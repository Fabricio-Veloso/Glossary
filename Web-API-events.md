# **Glossário — Eventos (Event System da Web API)**

Eventos são um dos pilares da Web.  
Eles permitem que sua aplicação **reaja** ao que acontece no navegador: cliques, teclas, mudanças, carregamento, movimento, timers, redes, visibilidade, foco, etc.

Este guia explica o sistema de eventos de cima para baixo, incluindo o que você realmente precisa para construir UIs dinâmicas e editores como o que está criando.

---

# **1. O que é um Evento?**

Um evento é um **sinal emitido pelo navegador** informando que “algo aconteceu”.  
Exemplos:

- O usuário clicou (`click`)
- O DOM carregou (`DOMContentLoaded`)
- O mouse entrou em um elemento (`mouseenter`)
- Uma tecla foi pressionada (`keydown`)
- Algo mudou em um `<input>` (`input`)
- Um elemento ganhou foco (`focus`)
- A aba foi trocada (`visibilitychange`)

Eventos são objetos — instâncias de classes como:

- `MouseEvent`
- `KeyboardEvent`
- `InputEvent`
- `FocusEvent`
- `DragEvent`
- `CustomEvent`

Todos herdam de:

```
EventTarget → Event → (MouseEvent, KeyboardEvent, ...)
```

---

# **2. Quem pode emitir/receber eventos?**

Todo objeto que implementa **EventTarget**, incluindo:

- `document`
- `window`
- qualquer elemento (`div`, `p`, `input`)
- `XMLHttpRequest`
- `WebSocket`
- `AbortController.signal`

Você pode ouvir eventos em **nodes específicos**, ou no documento inteiro:

```
element.addEventListener("click", handler);
document.addEventListener("keydown", handler);
window.addEventListener("resize", handler);
```

---

# **3. Como adicionar e remover listeners**

A API moderna (e padrão):

```
el.addEventListener("click", handler);
el.removeEventListener("click", handler);
```

Nunca use `onclick = ...` — sobrescreve handlers e é difícil de escalar.

---

# **4. Fases do evento: Captura, Alvo, Bublle**

Um conceito crucial para dominar UIs complexas.

Quando um evento dispara, ele percorre 3 etapas:

```
1. Captura   (de window → document → elemento)
2. Alvo      (no próprio elemento clicado)
3. Bublle    (do elemento → document → window)
```

Assim o navegador consegue:

- detectar um clique num elemento específico
- permitir delegação de eventos
- aplicar comportamento padrão

### **Exemplo com captura:**

```
el.addEventListener("click", handler, { capture: true })
```

Captura quase nunca é necessária, exceto em casos muito específicos.

---

# **5. Event Bubbling (bolha)**

É a parte mais usada.

Um clique em um `<button>` dentro de um `<div>` sobe até o `<div>`, `<body>` e `document`.

Isso permite coisas como:

## **Delegação de eventos (essencial para editores)**

```
document.addEventListener("click", e => {
  if (e.target.matches(".item")) {
    console.log("clicou num item");
  }
});
```

Você usa isso em:

- seleção de elementos
- arrastar e soltar
- menus contextuais
- editores complexos como o seu

---

# **6. `e.target` vs `e.currentTarget`**

Um dos conceitos mais confusos.

### **e.target**  
É o elemento REAL que recebeu o clique.

### **e.currentTarget**  
É o elemento onde o listener está registrado.

```
<div id="container">
  <button id="b">x</button>
</div>

container.addEventListener("click", e => {
  console.log(e.target);        // o botão
  console.log(e.currentTarget); // o container
});
```

No seu editor, você usa:

```
const selected = e.target.closest('.cert-element');
```

Isso funciona porque você entende que **target pode estar lá dentro**, mas você sobe até o elemento correto.

---

# **7. Prevenir comportamento padrão**

```
e.preventDefault()
```

Usado em:

- impedir envio de formulário
- bloquear seleção de texto
- impedir rolagem
- customizar comportamento de links

---

# **8. Parar a propagação (importante em UIs)**

```
e.stopPropagation()
```

Isso impede que o evento continue subindo.

Muito útil em:

- menus que fecham ao clicar fora
- cliques em overlays
- casos onde clicar dentro do container não deve acionar handlers externos

---

# **9. Tipos principais de eventos**

## **9.1 Mouse**

```
click
dblclick
mousedown
mouseup
mousemove
mouseenter
mouseleave
mouseover
contextmenu
```

## **9.2 Teclado**

```
keydown
keyup
keypress (obsoleto)
```

## **9.3 Formulários / Inputs**

```
input
change
submit
focus
blur
```

## **9.4 Página / Documento**

```
DOMContentLoaded
load
visibilitychange
scroll
resize (via window)
```

## **9.5 Clipboard**

```
copy
cut
paste
```

## **9.6 Drag & Drop**

```
dragstart
drag
dragover
drop
dragleave
dragend
```

## **9.7 Custom Events**

Você pode criar seus próprios eventos:

```
const ev = new CustomEvent("meu-evento", { detail: { x: 10 } });
element.dispatchEvent(ev);
```

---

# **10. Estrutura do objeto Event**

Eventos possuem várias propriedades úteis:

```
e.type
e.target
e.currentTarget
e.timeStamp
e.bubbles
e.cancelable
```

Eventos específicos têm extras:

### **MouseEvent**
```
e.clientX
e.clientY
e.button
e.altKey
e.ctrlKey
e.shiftKey
```

### **KeyboardEvent**
```
e.key
e.code
e.ctrlKey
e.repeat
```

---

# **11. Eventos em sistemas de UI complexos (seu caso)**

Quando você cria:

- editores
- sidebars dinâmicas
- seletores e caches de elementos
- drag and drop
- mudanças visuais

Você vai combinar:

### ✔ Delegação (`document.addEventListener(...)`)  
### ✔ Uso inteligente de `target` e `currentTarget`  
### ✔ Parar propagação quando necessário  
### ✔ Eventos customizados  
### ✔ Eventos de input para refletir mudanças no DOM  

---

# **12. Armadilhas comuns**

- Colocar muitos listeners em elementos pequenos → prefira delegação.  
- Usar `onclick` e perder estados.  
- Não remover listeners ao destruir componentes.  
- Não chamar `preventDefault` em eventos de formulário quando necessário.  
- Confundir `target` com `currentTarget`.

---

# **Resumo para lembrar sempre**

**Eventos são o sistema nervoso da página.  
Tudo o que o usuário faz emite sinais.  
Sua função como desenvolvedor é ouvir esses sinais e reagir.**

---

# **Fim**
