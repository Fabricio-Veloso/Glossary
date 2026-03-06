# FastAPI

## Default sequence:
```lua
cliente
   ↓
TCP
   ↓
uvicorn
   ↓
ASGI call
   ↓
Starlette router
   ↓
FastAPI dependency resolver
   ↓
Pydantic validation
   ↓
sua função
   ↓
serialização JSON
   ↓
response
   ↓
uvicorn
   ↓
cliente
```
---

## 1. O problema que async resolve

- Então é importante estabelecer um modelo mental correto de async, porque FastAPI depende diretamente disso. Sem entender esse ponto, é fácil criar código que parece assíncrono, mas na prática bloqueia o servidor.

Vou construir a explicação do zero.


Imagine um servidor simples que atende requisições:

```python
def handler():
    data = database.query()
    return data
```

Se `query()` demora 200 ms, o servidor fica parado esperando.

Se 1000 usuários fizerem requisições ao mesmo tempo:

```
request 1 → espera
request 2 → espera
request 3 → espera
```

O throughput cai drasticamente.

A solução tradicional foi **threads**.

```
thread 1 → request A
thread 2 → request B
thread 3 → request C
```

Problemas:

- custo de memória  
- troca de contexto  
- escalabilidade limitada  

---

## 2. O modelo async

Async usa **cooperative multitasking**.

Uma função pode **pausar voluntariamente**.

Exemplo:

```python
async def handler():
    data = await database.query()
    return data
```

Aqui acontece algo importante:

`await`

significa:

> "vou esperar algo externo, pode executar outra coisa enquanto isso".

Então o servidor faz:

```
request A → pausa
request B → executa
request C → executa
```

Tudo em **uma única thread**.

---

## 3. O event loop

Quem coordena isso é o **event loop**.

Ele funciona como um **scheduler**.

Pseudo-lógica:

```
loop:
   pega coroutine pronta
   executa até encontrar await
   pausa
   executa próxima coroutine
```

Então você tem:

```
task A
task B
task C
task D
```

Todas compartilhando o mesmo loop.

**Uvicorn usa exatamente esse modelo.**

---

## 4. O que `async def` realmente faz

Uma função `async` **não executa imediatamente**.

Ela cria uma **coroutine**.

Exemplo:

```python
async def f():
    return 1
```

Chamar:

```python
f()
```

retorna:

```
<coroutine object>
```

Para executar precisa:

```python
await f()
```

ou

```python
loop.run_until_complete(f())
```

---

## 5. Como isso se encaixa no FastAPI

Quando você escreve:

```python
@app.get("/")
async def route():
    data = await db.fetch()
    return data
```

Fluxo:

```
uvicorn event loop
     ↓
cria coroutine da rota
     ↓
executa até await
     ↓
libera o loop
     ↓
outra request executa
```

Isso permite **altíssima concorrência**.

---

## 6. O erro clássico

Muita gente escreve:

```python
@app.get("/")
async def route():
    data = requests.get("https://api.com")
    return data.json()
```

Mas `requests` é **bloqueante**.

Então acontece:

```
event loop
   ↓
requests.get()
   ↓
loop bloqueado
```

Todas as outras requests ficam esperando.

Async **deixa de funcionar**.

---

## 7. Biblioteca correta

Para HTTP async:

- httpx  
- aiohttp  

Exemplo:

```python
import httpx

@app.get("/")
async def route():
    async with httpx.AsyncClient() as client:
        r = await client.get("https://api.com")
    return r.json()
```

Agora sim:

```
await → libera event loop
```

---

## 8. Quando usar `def` em FastAPI

Essa parte é pouco explicada.

Se sua função **não usa await**, use `def` normal.

```python
@app.get("/")
def route():
    return {"ok": True}
```

FastAPI executa isso em **threadpool automaticamente**.

Internamente:

```python
run_in_threadpool(route)
```

Isso evita bloquear o event loop.

---

## 9. Regra prática

Use:

### `async def`

quando usa:

- chamadas HTTP async  
- drivers async  
- operações de rede  
- streaming  
- websocket  

### `def`

quando faz:

- CPU  
- lógica pura  
- libs bloqueantes  
- ORM síncrono (ex: SQLAlchemy clássico)  

---

## 10. Um detalhe arquitetural importante

FastAPI suporta **misturar os dois modelos**.

```
async routes
sync routes
```

O framework gerencia isso.

```
async → event loop
sync  → threadpool
```

Isso simplifica bastante a **migração de código antigo**.

---

## 11. Um insight importante sobre performance

O ganho de async **não vem de código mais rápido**.

Vem de:

```
menos tempo ocioso esperando IO
```

Ideal para:

- APIs  
- microservices  
- gateways  
- proxies  
- websockets  

Não ajuda muito em:

- CPU pesada  
- machine learning  
- processamento de imagem  
