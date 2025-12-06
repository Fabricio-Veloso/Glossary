# Glossário geral de WEB-API, JS, HTML, CSS.

# HTML 
# 1. Como `<div>` funciona, como o fluxo da página influencia o layout e como `position: relative` se encaixa nisso

Este guia explica de forma direta como `<div>` se comporta, como o CSS controla o fluxo dos elementos, e qual papel o `position: relative` desempenha — além de mostrar como adicionar novos elementos dentro de uma `<div>`.

---

## 1. Como uma `<div>` funciona por padrão

Uma `<div>` é um **elemento de nível de bloco (block-level)**. Isso significa:

- Ela ocupa **100% da largura disponível**.
- Ela faz uma **quebra de linha antes e depois** de si mesma.
- Seus filhos são renderizados **de cima para baixo**, seguindo o “fluxo normal” da página.

Esse comportamento só muda quando você aplica CSS que altera:

    - display (`flex`, `inline-block`, `grid`…)
- position (`absolute`, `relative`, `fixed`…)
    - float
    - transformações especiais

    ---

## 2. Por que seus elementos às vezes ficaram um em cima do outro?

    No seu layout, isto aqui controla a disposição horizontal:

    ```html
    <div id="preview-wrapper"
    style="position:relative; margin-top:20px; display:flex; gap:16px;">
    ```

    O display:flex é o que coloca os itens lado a lado.

    Se você remove essa div ou remove o display:flex, cada filho volta para o comportamento padrão de bloco → fica um em cima do outro.

    Ou seja, o “culpado” não é o position:relative, mas sim o fluxo normal que volta quando o flex desaparece.

    ---

## 3. O que o position: relative realmente faz

    Muita gente se confunde porque position:relative não mexe visivelmente no layout sozinho. Ele faz duas coisas:

### 3.1. Criar um "contexto de posicionamento"

    Quando um elemento pai tem:

    position: relative;


    Isso permite que seus elementos absolutamente posicionados (position:absolute) usem esse pai como referência para:

    - top  
    - left  
    - right  
    - bottom  

    Sem isso, eles usam o body ou o ancestral posicionado mais próximo.

    No seu editor, os textos arrastáveis usam isso para ficarem dentro da imagem.

### 3.2. Permitir deslocamentos opcionais

    Se você colocar:
    ```css
    position:relative;
top:10px;
left:20px;
```

Ele continua ocupando seu espaço normal, mas o visual dele é deslocado por cima do layout.

Isso é útil para ajustes finos, mas não para layouts estruturais.

### Resumo rápido:

Position Mantém espaço original? Pode usar top/left? Sai do fluxo normal?
| Position        | Mantém espaço original? | Pode usar top/left? | Sai do fluxo normal? |
| --------------- | ----------------------- | ------------------- | -------------------- |
| static (padrão) | sim                     | não                 | não                  |
| relative        | sim                     | sim                 | não                  |
| absolute        | não                     | sim                 | sim                  |
| fixed           | não                     | sim                 | sim                  |
| sticky          | sim/não                 | sim                 | parcialmente         |


---

## 4. Por que tanta div com position:relative no seu código?

Porque no seu editor:

- Uma div pai define um contexto de coordenadas.  
- Os textos arrastáveis dentro dela são position:absolute.  
- Eles precisam desse “mundo local” para se mover sem sair da borda da imagem.

Sem o position:relative no contêiner da imagem, arrastar elementos se tornaria impossível.

---

## 5. Como adicionar novos elementos dentro de uma <div>

### 5.1. Via HTML direto

```html
<div class="preview-container">
<div class="label">Nome do participante</div>
<div class="label">Cidade</div>
</div>
```

### 5.2. Via JavaScript (mais comum em editores visuais)

```js
const container = document.getElementById("preview-container");

const novo = document.createElement("div");
novo.className = "label";
novo.textContent = "Novo campo";
novo.style.position = "absolute"; // para arrastar
novo.style.top = "100px";
novo.style.left = "80px";

container.appendChild(novo);
```

### 5.3. Via DOM + template

```html
<template id="label-template">
<div class="label" style="position:absolute;">Texto</div>
</template>
```

```js
const tpl = document.getElementById("label-template");
const clone = tpl.content.cloneNode(true);
clone.querySelector(".label").textContent = "CPF";
document.getElementById("preview-container").appendChild(clone);
```

---

## 6. Como as <div> e o display afetam totalmente a posição

### 6.1. Fluxo normal (“um abaixo da outra”)

div { display:block; }


### 6.2. Lado a lado

.container {
display:flex;
}


### 6.3. Layout em colunas

.container {
display:grid;
        grid-template-columns: 1fr 1fr;
}


### 6.4. Sobreposição manual

.child {
position:absolute;
top:0;
left:0;
}


---

## 7. Por que às vezes “nada acontece” ao tirar position:relative?

Porque position:relative não altera nada visualmente por padrão.

Você só nota diferença quando:

- existe um filho com position:absolute, ou
- você usa top/left/right/bottom.

Exemplo:

```html
<div style="position:relative;">
<div style="position:absolute; top:20px; left:20px;">
aparece exatamente 20px dentro do pai
</div>
</div>
```

Se você remove o position:relative do pai:

- A referência muda para o body  
- O elemento “some” da área onde deveria estar  
- O layout interno perde o alinhamento  

Se não existir absolutamente posicionado dentro → nada muda mesmo.

---

## 8. Explicação visual simples

[ PAI (position:relative) ]
└── [ FILHO (position:absolute; top:10; left:10) ]


O filho usa o PAI como mapa cartesiano.  
Se o pai não for relative/absolute/fixed/sticky → o mapa vira o BODY.

---

## 9. Checklist mental para entender layout

- O elemento é block, inline, flex ou grid?  
- Ele está no fluxo normal ou foi removido com position:absolute?  
- Ele tem um pai com posição relativa para servir de referência?  
- Existe display:flex ou grid alterando a disposição horizontal/vertical?  
- Ele está dentro de outros elementos que controlam largura e altura?  

---

## 10. Resumo final

- `<div>` é bloco: ocupa a linha inteira e joga o próximo para baixo.  
- `display:flex` → coloca elementos lado a lado.  
- `position:relative` → não muda visualmente, mas cria um sistema de coordenadas.  
- `position:absolute` → remove o elemento do fluxo e usa o pai posicionado como referência.  
- Remover as `<div>` externas tirou o flex, então os elementos voltaram a empilhar.  
- Adicionar novos elementos dentro de uma `<div>` é só inserir via HTML ou `appendChild()`.  

# JavaScript

## Object, Map e Set

Este glossário oferece uma visão clara e prática dos principais recursos de `Object`, `Map` e `Set`.  
Focado no uso moderno do JavaScript e especialmente útil para manipulação dinâmica de configurações, edição de elementos e criação de sistemas reativos simples.

---

### 1. `Object` – A Base de Tudo

`Object` é o tipo fundamental para estruturas de dados do JavaScript.  
Todo objeto simples `{}` herda dele, e ele fornece métodos extremamente úteis para manipulação estrutural.

---

### 1.1 `Object.keys(obj)`
Retorna um array contendo **todas as chaves** do objeto.

```
Object.keys({ a: 1, b: 2 });  
// ["a", "b"]
```

**Quando usar:** iterar sobre chaves, validar propriedades, contar campos.

---

### 1.2 `Object.values(obj)`
Retorna um array contendo **todos os valores**.

```
Object.values({ a: 1, b: 2 });
// [1, 2]
```

**Quando usar:** análises nos valores, map/filter apenas nos valores.

---

### 1.3 `Object.entries(obj)`
Retorna pares `[chave, valor]`.

```
Object.entries({ a: 1, b: 2 });
// [["a", 1], ["b", 2]]
```

**Quando usar:** cadastro dinâmico, transformação de dados, criação de inputs dinâmicos.

---

### 1.4 `Object.fromEntries(array)`
Transforma um array de pares `[chave, valor]` novamente em objeto.

```
Object.fromEntries([
  ["a", 1],
  ["b", 2]
]);
// { a: 1, b: 2 }
```

**Quando usar:** reconstruir objetos após filtros, maps e transformações.

---

### 1.5 `Object.assign(target, ...sources)`
Copia propriedades de outros objetos para o alvo.

```
const merged = Object.assign({}, defaults, userConfig);
```

**Quando usar:** merges rasos, aplicar defaults, sobrescrever configs.

---

### 1.6 `Object.freeze(obj)`
Torna o objeto totalmente imutável.

```
const cfg = Object.freeze({ theme: "dark" });
```

**Quando usar:** constantes, configs estáveis.

---

### 1.7 `Object.seal(obj)`
Impede adicionar/remover chaves, mas permite alterar valores existentes.

**Quando usar:** estruturas fixas com valores variáveis.

---

### 1.8 `Object.getOwnPropertyDescriptors(obj)`
Retorna detalhes completos sobre cada propriedade.

```
Object.getOwnPropertyDescriptors({ a: 1 });
```

**Quando usar:** sistemas reativos, clones profundos, proxies, validação profunda.

---

## 2. `Map` – Tabelas de Chave → Valor Modernas

`Map` é uma estrutura mais poderosa do que objetos simples quando a chave **não** é apenas texto.

---

### 2.1 Características principais

- aceita *qualquer* tipo de chave (strings, números, objetos, funções, elementos DOM)
- preserva a ordem de inserção
- fácil de iterar
- não tem colisões de propriedades (como `toString`)

---

### 2.2 Exemplo básico

```
const map = new Map();
map.set("fontSize", 22);
map.set(domElement, { x: 10, y: 20 });

map.get("fontSize"); // 22
map.get(domElement); // { x: 10, y: 20 }
```

---
### 2.3 Funções como Parâmetros (Callback Functions)

#### 1. O que significa "passar uma função como parâmetro"?
Em JavaScript, funções **são valores** — da mesma forma que números, strings e objetos.  
Isso significa que você pode:
- Guardar funções em variáveis
- Passar funções para outras funções
- Retornar funções de dentro de funções

Quando você passa uma função como parâmetro, está dizendo:

> “Ei, quando isso acontecer, execute *essa* função que estou te entregando.”

Esse padrão é essencial para:
- eventos (`addEventListener`)
- callbacks (`forEach`, `map`, `setTimeout`)
- funções reutilizáveis
- programação assíncrona (Promises)

---

#### 2. Callback Function
Um **callback** é simplesmente uma função passada como argumento para outra função.

Exemplo simples:

```js
function fazerAlgo(callback) {
  callback("executado!");
}

fazerAlgo(msg => console.log(msg));
```

---

#### 3. Diferença entre "passar a função" e "executar a função"

##### Passar referência da função  
Você entrega *a função em si*, sem executá-la:

```js
button.addEventListener('click', minhaFuncao);
```

Aqui o navegador decide **quando** chamar.

##### Executar imediatamente  
Você chama a função e passa o resultado (o que geralmente está errado neste contexto):

```js
button.addEventListener('click', minhaFuncao());
```

---

#### 4. Funções anônimas vs. funções nomeadas
Eventualmente você usa funções **anônimas** (criadas na hora):

```js
button.addEventListener('click', () => console.log("clicado"));
```

Ou funções **nomeadas**, boas para reutilização:

```js
function handleClick() {
  console.log("clicado");
}

button.addEventListener('click', handleClick);
```

---

#### 5. Como isso aparece no seu exemplo real

##### Seu primeiro exemplo (correto):
```js
const onChange = (newValue) => {
  attribute.apply(selectedElementId, newValue);
};
```

Aqui `onChange` é **uma função passada para outra API** no momento adequado.

---

#### 6. Como aplicar corretamente no segundo exemplo
Seu código atual está assim:

```js
document.getElementById('sb_save')
  .addEventListener('click', new_value => {
      saveSidebarChanges(elements_config)
  });
```

Isso já é **passar uma função como parâmetro** — a função anônima `(new_value => {...})`.

Mas um ajuste deixa isso mais claro, reutilizável e idiomático:

##### Opção A — passar uma função nomeada (recomendado):
```js
export function enableSidebarSave(elements_config){
  function handleSaveClick() {
    saveSidebarChanges(elements_config);
  }

  document.getElementById('sb_save')
    .addEventListener('click', handleSaveClick);
}
```

##### Opção B — criar um "dispatcher" reutilizável
Padrão mais próximo do que você fez no `onChange`:

```js
export function enableSidebarSave(elements_config){
  const onSave = () => saveSidebarChanges(elements_config);

  document.getElementById('sb_save')
    .addEventListener('click', onSave);
}
```

---

#### 7. Por que isso importa?
- Reduz repetição de código  
- Separa *lógica* de *evento*
- Facilita depuração
- Cria funções pequenas e focadas
- Torna o código mais previsível e reutilizável

---

#### 8. Regra mental simples
> “Quando a função depende de quando algo vai acontecer (ex: clique), passe a **referência da função** e não execute diretamente.”

---

#### 9. TL;DR (resumo rápido)
- JS trata funções como valores ⇒ você pode passá-las como parâmetros.  
- `addEventListener` sempre espera uma **função**, não o resultado dela.  
- Evite executar funções dentro do próprio argumento.  
- Nomear callbacks geralmente deixa o código mais limpo e fácil de manter.



---

## 2.3 Quando usar `Map`

- configs associadas a elementos DOM
- caching
- registrar componentes criados dinamicamente
- evitar colisão de nomes em objetos simples
- chave precisa ser um objeto (ex.: o próprio elemento HTML selecionado)

---

## 3. `WeakMap` – Chaves Fracas Associadas a Objetos

Igual ao `Map`, mas só aceita **objetos** como chave, e essas chaves **não impedem garbage collection**.

---

## 3.1 Exemplo

```
const meta = new WeakMap();
meta.set(domElement, { config: { x: 10, y: 20 } });
```

Quando o elemento sai do DOM, sua entrada no WeakMap desaparece automaticamente.

---

## 3.2 Quando usar

- anexar configs a elementos DOM sem risco de vazamento de memória
- armazenar estado interno de componentes
- estruturas reativas e editores de conteúdo

---

## 4. `Set` – Coleção de Valores Únicos

`Set` funciona como um array, mas **não permite valores duplicados**.

---

## 4.1 Exemplo básico

```
const s = new Set();
s.add("nome");
s.add("nome"); // ignorado
s.add("cor");

console.log([...s]); // ["nome", "cor"]
```

---

## 4.2 Quando usar

- evitar duplicação
- registrar elementos selecionados
- registrar componentes ativos
- conjuntos de IDs ou classes
- filtros únicos (como lista de fontes usadas no template)

---

## 5. Diferença Geral entre Object, Map e Set

| Estrutura | Chaves | Ordem | Aceita objeto como chave? | Principal uso |
|----------|--------|--------|----------------------------|----------------|
| Object | strings/símbolos | geralmente sim | não | dados estáticos, configs simples |
| Map | qualquer coisa | sim | sim | tabelas dinâmicas, chaves complexas |
| WeakMap | objetos | sim | **somente objetos** | metadados ligados ao DOM |
| Set | valores únicos | sim | — | coleções sem duplicados |

---

## 6. Dicas para Editor de Layout (caso de uso real)

### ✔ Para guardar configs do JSON por ID:
Use **Object**.

### ✔ Para ligar um DOM element à sua configuração:
Use **WeakMap**.

Exemplo:

```
const elementConfig = new WeakMap();

function attachElementConfig(el, config) {
  elementConfig.set(el, config);
}

function getConfig(el) {
  return elementConfig.get(el);
}
```

### ✔ Para registrar atributos suportados (como `fontSize`, `color`):
Use um **Object simples**, como seu `attributeMap`.

### ✔ Para listas de fontes únicas:
Use `Set`.

---

## 7. Referência rápida (cola fácil)

- `Object.keys(obj)` → chaves  
- `Object.values(obj)` → valores  
- `Object.entries(obj)` → pares chave + valor  
- `Object.fromEntries(arr)` → array → objeto  
- `Object.assign(a, b)` → merge  
- `Object.freeze(obj)` → imutável  
- `Map` → tabela chave-valor moderna  
- `WeakMap` → metadados atrelados ao DOM sem vazamentos  
- `Set` → coleção sem duplicados  
---

# DOM Core API

Este documento resume, de forma clara e completa, os conceitos fundamentais da **DOM Core API**, a base de qualquer manipulação de HTML via JavaScript.

Ele explica:

- o que é DOM
- como a árvore DOM funciona
- como criar, remover e modificar elementos
- como navegar pela árvore
- como alterar atributos, classes e estilos
- APIs essenciais para manipulação de nós

---

## 1. O que é DOM

DOM = **Document Object Model**  
É a representação da página HTML como uma **árvore de nós** manipulável por JavaScript.

Cada tag vira um objeto na memória:

```js
<div> → HTMLDivElement
<span> → HTMLSpanElement
input → HTMLInputElement
#text → TextNode
```

Você manipula essa árvore usando a **DOM Core API**, que o navegador fornece.

---

## 2. Seleção de elementos

Métodos principais:

### **document.getElementById(id)**  
Retorna 1 elemento com ID específico.

### **document.querySelector(seletor)**  
Retorna o **primeiro** elemento que bate com um seletor CSS.

### **document.querySelectorAll(seletor)**  
Retorna **todos** os elementos.

Exemplo:

```js
const el = document.querySelector(".card");
```

---

## 3. Criação de elementos

Criar um elemento novo na memória:

```js
const div = document.createElement("div");
```

Criar um nó de texto:

```js
const txt = document.createTextNode("Olá");
```

---

## 4. Inserção na árvore

### **appendChild()**

```js
parent.appendChild(child);
```

### **prepend()** – coloca no início  
### **before() / after()** – insere adjacente  
### **remove()** – remove do DOM

---

## 5. Atributos e propriedades

## Setando atributos HTML:

```js
el.setAttribute("src", "/img.png");
el.getAttribute("value");
```

## Propriedades DOM (preferível):

```js
el.src = "/img.png";
el.value = "Texto";
```

---

## 6. Classes

Usando `classList` (moderno e seguro):

```js
el.classList.add("ativo");
el.classList.remove("hidden");
el.classList.toggle("selected");
```

---

## 7. Estilos (CSS inline)

```js
el.style.color = "red";
el.style.fontSize = "20px";
el.style.display = "flex";
```

Para vários estilos de uma vez:

```js
Object.assign(el.style, {
  color: "blue",
  fontWeight: "bold"
});
```

---

## 8. Dimensões e posição

```js
el.offsetWidth
el.offsetHeight
el.getBoundingClientRect() // posição, tamanho e scroll
```

---

## 9. Conteúdo interno

### **textContent** (texto puro)

```js
el.textContent = "Olá";
```

### **innerHTML** (insere HTML)

```js
el.innerHTML = "<strong>Olá</strong>";
```

### **innerText**  
Menos usado (depende do layout).

---

## 10. Navegação na árvore

## Subindo e descendo:

```js
el.parentNode
el.children
el.firstChild
el.lastChild
```

## Navegando irmãos:

```js
el.nextSibling
el.previousSibling
```

## Filtrando só elementos:

```js
el.nextElementSibling
el.previousElementSibling
```

---

## 11. Clonagem

```js
const clone = el.cloneNode(true); // true = copia filhos
```

---

# 12. Trabalhando com dados em elementos

## data-attributes:

HTML:

```html
<div data-id="123"></div>
```

JS:

```js
el.dataset.id === "123"
el.dataset.id = "777"
```

---

## 13. Criar documentos inteiros dinamicamente

```js
const card = document.createElement("div");
card.className = "card";

const title = document.createElement("h2");
title.textContent = "Exemplo";

card.appendChild(title);
```

---

## 14. Reflow e Repaint (conceito avançado)

- **Reflow** → navegador recalcula o layout
- **Repaint** → navegador redesenha pixels

Mudanças no DOM podem causar reflows caros.  
Boas práticas:

- alterar style em lote  
- usar fragmentos  
- evitar mudanças repetidas no layout

---

## 15. DocumentFragment (ótimo para performance)

```js
const frag = document.createDocumentFragment();

for (let i = 0; i < 1000; i++) {
  const li = document.createElement("li");
  li.textContent = i;
  frag.appendChild(li);
}

ul.appendChild(frag);
```

---

## 16. Resumo das APIs essenciais

### Criar
- document.createElement
- document.createTextNode

### Inserir
- appendChild
- prepend
- before / after

### Modificar
- classList
- style
- setAttribute

### Selecionar
- querySelector / All
- getElementById

### Navegar
- parentNode
- children
- nextElementSibling

### Remover
- remove()

---
Esse conjunto é **a base de qualquer manipulação de HTML**.
Dominar esses pontos te deixa totalmente capaz de:
- gerar UIs dinâmicas
- montar painéis
- fazer editores visuais
- criar componentes de interface
- manipular elementos selecionados pelo usuário
---

