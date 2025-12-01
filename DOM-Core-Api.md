# GLOSSÁRIO — DOM Core API

Este documento resume, de forma clara e completa, os conceitos fundamentais da **DOM Core API**, a base de qualquer manipulação de HTML via JavaScript.

Ele explica:

- o que é DOM
- como a árvore DOM funciona
- como criar, remover e modificar elementos
- como navegar pela árvore
- como alterar atributos, classes e estilos
- APIs essenciais para manipulação de nós

---

# 1. O que é DOM

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

# 2. Seleção de elementos

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

# 3. Criação de elementos

Criar um elemento novo na memória:

```js
const div = document.createElement("div");
```

Criar um nó de texto:

```js
const txt = document.createTextNode("Olá");
```

---

# 4. Inserção na árvore

### **appendChild()**

```js
parent.appendChild(child);
```

### **prepend()** – coloca no início  
### **before() / after()** – insere adjacente  
### **remove()** – remove do DOM

---

# 5. Atributos e propriedades

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

# 6. Classes

Usando `classList` (moderno e seguro):

```js
el.classList.add("ativo");
el.classList.remove("hidden");
el.classList.toggle("selected");
```

---

# 7. Estilos (CSS inline)

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

# 8. Dimensões e posição

```js
el.offsetWidth
el.offsetHeight
el.getBoundingClientRect() // posição, tamanho e scroll
```

---

# 9. Conteúdo interno

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

# 10. Navegação na árvore

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

# 11. Clonagem

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

# 13. Criar documentos inteiros dinamicamente

```js
const card = document.createElement("div");
card.className = "card";

const title = document.createElement("h2");
title.textContent = "Exemplo";

card.appendChild(title);
```

---

# 14. Reflow e Repaint (conceito avançado)

- **Reflow** → navegador recalcula o layout
- **Repaint** → navegador redesenha pixels

Mudanças no DOM podem causar reflows caros.  
Boas práticas:

- alterar style em lote  
- usar fragmentos  
- evitar mudanças repetidas no layout

---

# 15. DocumentFragment (ótimo para performance)

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

# 16. Resumo das APIs essenciais

## Criar
- document.createElement
- document.createTextNode

## Inserir
- appendChild
- prepend
- before / after

## Modificar
- classList
- style
- setAttribute

## Selecionar
- querySelector / All
- getElementById

## Navegar
- parentNode
- children
- nextElementSibling

## Remover
- remove()

---

Esse conjunto é **a base de qualquer manipulação de HTML**.
Dominar esses pontos te deixa totalmente capaz de:
- gerar UIs dinâmicas
- montar painéis
- fazer editores visuais
- criar componentes de interface
- manipular elementos selecionados pelo usuário

Fim.
