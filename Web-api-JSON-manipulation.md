# Glossário Prático e Profundo: Manipulação de JSON em JavaScript + Web APIs

Este documento reúne conceitos, padrões e técnicas essenciais para trabalhar com JSON em JavaScript, tanto **em memória** quanto **no fluxo de Web APIs**.  
O foco é ser direto, altamente prático e aplicável a cenários reais de desenvolvimento web.

---

### 1. JSON não é um tipo do JavaScript (mas se converte facilmente)

JSON é apenas **texto**.  
Em JS, você transforma JSON ⇄ objeto com:

```js
const obj = JSON.parse(jsonString);       // texto → objeto
const json = JSON.stringify(obj);         // objeto → texto JSON

    Dica: JSON só aceita: number, string, boolean, null, arrays e objetos.
```
---
### 2. Estruturas JSON comuns (objeto vs lista de objetos)

```js
{
  "name": "Fab",
  "age": 30
}

{
  "elements": [
    { "id": "nome", "value": "Fabrício" },
    { "id": "Text-Info", "value": "informações..." }
  ]
}
```
Quase sempre você vai manipular listas de objetos como essa — especialmente para UI, configurações, formulários e APIs.

---
### 3. Buscas em arrays de objetos
Buscar o primeiro item por campo
```js
const item = json.elements.find(el => el.id === "nome");

Buscar todos

const items = json.elements.filter(el => el.type === "text");

Verificar existência

const exists = json.elements.some(el => el.id === "nome");
```
---
### 4. Atualização de itens dentro de JSON
Atualizar um item específico
```js
const id = "nome";

const updated = json.elements.map(el =>
  el.id === id
    ? { ...el, value: "Novo valor" }
    : el
);
```
- Regra de ouro moderna: atualize sem mutar sempre que puder.
- A imutabilidade evita bugs e facilita rastrear mudanças.

Atualizar mutando diretamente (às vezes faz sentido)
```js
const item = json.elements.find(el => el.id === "nome");
if (item) {
  item.value = "Novo valor";
}
```
Use mutação quando for local, controlado e sem impacto em estados compartilhados.

---
### 5. Remoção de itens
```js
json.elements = json.elements.filter(el => el.id !== "Text-Info");
```
### 6. Criação e inserção
```js
json.elements.push({
  id: "novo",
  type: "text",
  value: "exemplo",
  x: 0,
  y: 0
});
```
--- 
### 7. Clonagem de objetos JSON (muito importante!)

Evitar bugs por referência acidental:
Clone profundo simples
```js
const clone = structuredClone(obj);
```
Seguro, nativo e moderno.
Alternativa antiga
```js
const clone = JSON.parse(JSON.stringify(obj));
```
Perde funções, datas, undefined, etc.

---
### 8. JSON + DOM (interação típica em apps reais)
Selecionar um elemento com base num JSON
```js
const item = json.elements.find(e => e.id === "nome");
document.querySelector(`###${item.id}`).textContent = item.value;
```
Atualizar atributos dinamicamente
```js
const div = document.getElementById("sidebar");
div.style.left = `${item.x}px`;
div.style.top  = `${item.y}px`;
```
---
### 9. Fluxo completo de edição (padrão muito usado em apps)

    Seleciona um elemento no DOM

    Extrai o id dele

    Busca no JSON

    Joga no sidebar/editor

    Edita

    Atualiza o JSON com o novo valor

    Re-renderiza o DOM

Você provavelmente está montando exatamente esse fluxo.
### 10. Web APIs modernas e JSON
#### 10.1. Enviar JSON via fetch
```js
await fetch("/api/salvar", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify(json)
});
```
#### 10.2. Receber JSON
```js
const response = await fetch("/api/dados");
const data = await response.json();
```
    response.json() já converte o texto pra objeto JS.
### 11. Erros comuns ao trabalhar com JSON em Web APIs
Enviar objeto sem JSON.stringify

Erro frequente:
```js
body: obj // errado
```
Certo:
```js
body: JSON.stringify(obj)
```
Não colocar Content-Type correto
```js
headers: { "Content-Type": "application/json" }
```
Acessar resposta antes de converter
```js
const data = await response.json(); // obrigatório
```
JSON mal-formado no servidor

Falta vírgula, aspas duplas, valores inválidos → JSON.parse quebra.

---
### 12. Padronizando buscas por ID (melhor prática)

Criar helpers:
```js
const findById = (list, id) => list.find(x => x.id === id);
const updateById = (list, id, changes) =>
  list.map(el => el.id === id ? { ...el, ...changes } : el);
const removeById = (list, id) =>
  list.filter(el => el.id !== id);
```
Isso evita repetir lógica e erros de digitação.

---
### 13. Imutabilidade vs mutabilidade (quando usar cada uma)
Use imutabilidade quando:

    manipula estado global

    usa frameworks reativos

    precisa de undo/redo

    controla renderização ou diffs

Pode usar mutação quando:

    estado é local e temporário

    performance importa MUITO

    você conhece o escopo

---
### 14. Serialização e persistência
Salvar no localStorage
```js
localStorage.setItem("config", JSON.stringify(json));
```
Carregar
```js
const json = JSON.parse(localStorage.getItem("config"));
```

---
### 15. Buscar "rota" dentro de JSON aninhado (deep access)

JSON real às vezes é profundo:
```js
{
  "settings": {
    "editor": {
      "theme": {
        "name": "light"
      }
    }
  }
}
```
Acessar:
```js
const theme = json.settings?.editor?.theme?.name;
```
O ?. evita erros caso algum nível seja undefined.

---
### 16. Transformações úteis (map, reduce, sort)
Transformações com map

Extraindo apenas valores:
```js
const ids = json.elements.map(e => e.id);
```
Ordenar por campo
```js
json.elements.sort((a, b) => a.x - b.x);
```
Converter em objeto por ID (ótimo para busca rápida)
```js
const byId = json.elements.reduce((acc, el) => {
  acc[el.id] = el;
  return acc;
}, {});
```
---
### 17. Validação básica de JSON antes de usar
```js
try {
  const parsed = JSON.parse(text);
} catch (err) {
  console.error("JSON inválido", err);
}
```
---

### 18. Enviando e recebendo arrays grandes (técnicas práticas)

    compressão na API (gzip/brotli)

    paginação

    lazy-loading

    chunking

    diffs (enviar só mudanças)

Você só precisa disso quando a estrutura fica grande demais (100k+, por exemplo).
### 19. Padrões arquiteturais para manipular JSON em apps maiores
model.js

Funções para buscar, atualizar, remover elementos.
state.js

JSON atual carregado + eventos de mudança.
ui.js

Renderiza o DOM com base no JSON.
api.js

Carrega e salva JSON na Web API.
controller.js

Conecta UI → State → API.

Esse padrão evita que JSON e DOM fiquem misturados e bagunçados.

---
### 20. Dicas finais (vividas na prática)

    Sempre normalize estruturas quando possível (byId, list).

    JSON grande deve ser imutável ou parcialmente imutável.

    Evite “mutação silenciosa” que altera o estado sem você ver.

    Use helpers como findById e updateById.

    Prefira structuredClone para clonar objetos complexos.

    Lidando com Web APIs, padronize erros e responses.

    Sempre garanta que id → é único e sem espaços.

    Trate JSON como estado, não apenas como dado.
---
