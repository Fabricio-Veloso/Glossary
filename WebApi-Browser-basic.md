# Glossário – Web API aplicada a FileReader, Eventos e Inputs de Arquivo

---

## 1. Web API (Contexto Geral)
**O que é:**  
Conjunto de funcionalidades que o navegador expõe ao JavaScript, permitindo interação com:
- DOM (Document Object Model)
- Eventos
- Rede (Fetch, WebSockets)
- Arquivos
- Canvas, Áudio, Vídeo etc.

**Por que importa aqui:**  
O código fornecido usa vários recursos da Web API:
- Eventos (`addEventListener`)
- Sistema de arquivos virtual do input (`input.files`)
- FileReader (leitura de arquivos no cliente)
- Propriedade `target` do objeto de evento

Esses recursos **não fazem parte do JavaScript puro** — são funcionalidades oferecidas pelo navegador.

---
## 2. Input de Arquivo (`<input type="file">`)
**Origem:** DOM API.

**Descrição:**  
Um `<input type="file">` permite selecionar arquivos do computador.  
Quando o usuário escolhe um arquivo, o navegador preenche:

```js
input.files // FileList
```
FileList é similar a um array e contém objetos File.
Cada File inclui:
```js
    nome

    tamanho

    tipo MIME (ex: image/png)

    conteúdo acessível somente via FileReader.

Uso no código:

const file = e.target.files[0];

e.target é o próprio input.
files[0] é o primeiro arquivo selecionado.


---


## 3. Eventos e `addEventListener`
**Origem:** DOM Events API.

**Descrição:**  
Elementos DOM podem registrar callbacks para eventos usando:

```js
element.addEventListener(tipo, callback);
```
Quando o evento dispara:

    o navegador cria um objeto Event

    o envia como argumento para o callback

No seu caso:

fundoInput.addEventListener('change', function(e) { ... });

Evento "change":
Disparado quando o valor do input muda, o que inclui seleção de arquivos.


---


## 4. O objeto de evento (`e`)
**Origem:** Criado pelo navegador (DOM Event API).

**Descrição:**  
`e` é apenas o nome da variável que recebe o objeto `Event` criado automaticamente.  
Pode ser chamado de qualquer nome:

```js
function(event) {}
function(evt) {}
function(x) {}
```
Esse objeto contém informações sobre o que ocorreu no evento.


---


## 5. `e.target`
**Origem:** Interface `Event`.

**Descrição:**  
`target` é sempre o **elemento DOM que disparou o evento**.

Exemplo:
```js
e.target // <input type="file">

Por isso funciona:

e.target.files

Ele permite acessar propriedades específicas do elemento que originou o evento.
```

---


## 6. `FileReader`
**Origem:** File API (Web API).

**Descrição:**  
Permite ler arquivos selecionados pelo usuário.  
O JavaScript não pode acessar arquivos do sistema diretamente por segurança; o FileReader fornece uma maneira controlada de acesso ao conteúdo.

**Criação:**
```js
const reader = new FileReader();
```
Principais eventos:

    onload → leitura completa

    onerror → falha

    onprogress → progresso da leitura


---


## 7. `reader.readAsDataURL(file)`
**Descrição:**  
Converte o arquivo para uma string DataURL. Exemplo:

data:image/png;base64,iVBORw0KGgoAAA...


Esse formato pode ser usado diretamente em:
- `img.src`
- pré-visualizações
- armazenamento temporário

Uso no código:
```js
reader.onload = function(event) {
    backgroundImg.src = event.target.result;
};

event.target.result contém o DataURL final.
```

---


## 8. `backgroundImg.onload`
**Origem:** HTMLImageElement API.

**Descrição:**  
Executado quando a imagem termina de carregar no navegador.  
Permite rodar lógica dependente da imagem renderizada.

Exemplo do código:
```js
backgroundImg.onload = function() {
    initializePositions();
};
```

---


## 9. Fluxo Completo (Resumo Operacional)
1. Usuário seleciona arquivo → evento `change`.
2. Navegador cria um objeto `Event` → enviado como `e`.
3. `e.target` aponta para o `<input>`.
4. `e.target.files[0]` retorna o arquivo escolhido.
5. Cria-se um `FileReader`.
6. `readAsDataURL` converte o arquivo para DataURL.
7. `reader.onload` recebe o resultado.
8. A imagem recebe esse DataURL no `src`.
9. Quando a imagem carrega → `backgroundImg.onload`.
10. `initializePositions()` é executado.

## 10. Código original comentado

```js
fundoInput.addEventListener('change', function(e) {
    const file = e.target.files[0];

    if (!file || !file.type.startsWith('image/')) return;

    const reader = new FileReader();

    reader.onload = function(event) {
        backgroundImg.src = event.target.result;
        backgroundImg.style.display = 'block';

        if (editorContainer) {
            editorContainer.style.display = 'block';
        }

        if (saveMessage) {
            saveMessage.style.display = 'none';
        }

        backgroundImg.onload = function() {
            initializePositions();
        };
    };

    reader.readAsDataURL(file);
});
```
