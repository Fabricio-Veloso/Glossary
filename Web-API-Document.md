
# **Glossário — `Document` (Web API)**

Este glossário aprofunda o objeto **`document`**, um dos elementos centrais da Web API.  
Pense nele como **a porta de entrada para toda manipulação do conteúdo da página** — você sempre começa por ele.

---

# **1. O que é o `document`**

O `document` é um objeto que representa **todo o documento HTML carregado no navegador**.  
Ele é a implementação concreta da interface **`Document`**, que por sua vez herda de `Node`, `EventTarget`, etc.

Em resumo:

- **Representa o HTML inteiro.**
- **Fornece métodos para buscar, criar e manipular elementos.**
- **Permite ouvir eventos globais (como carregamento do DOM).**
- **Gerencia estados como visibilidade, título, cookies e `<head>`/`<body>`.**

---

# **2. Linha de herança do `document`**

Saber essa cadeia evita confusão sobre "por que o document tem esse método?".

```
EventTarget
  ↑
Node
  ↑
Document
  ↑
HTMLDocument (para documentos HTML)
  ↑
document  (instância real)
```

Isso explica por que você pode fazer:

- `document.addEventListener(...)` → veio de **EventTarget**
- `document.childNodes` → veio de **Node**
- `document.getElementById` → veio de **Document**

---

# **3. Seleção de elementos via `document`**

## **3.1 Métodos clássicos**
Esses vieram da época pré-Selectors API:

```
document.getElementById("id")
document.getElementsByClassName("class")
document.getElementsByTagName("div")
```

- Muito rápidos
- Retornam coleções "vivas" (atualizam automaticamente)

---

## **3.2 Métodos modernos (Selectors API)**

```
document.querySelector(".classe")
document.querySelector("#id .child")
document.querySelectorAll("section > p")
```

- Extremamente flexíveis
- `querySelectorAll` retorna NodeList estático

Esse é o padrão moderno para quase tudo.

---

# **4. Criar elementos com `document`**

Esse é o grande ponto que você comentou — e é aqui que tudo começa a fazer sentido.

```
const div = document.createElement("div");
div.textContent = "Olá";
document.body.appendChild(div);
```

Criar ≠ colocar na página.  
Criar é só **gerar o objeto**. Aparecer na página = usar `appendChild`.

## **Outros métodos úteis**

```
document.createTextNode("texto puro")
document.createComment("comentário")
document.createDocumentFragment()
```

### **DocumentFragment**  
Um container leve para montar trechos de DOM em memória sem causar reflows na página.  
Muito importante em performance e renderizações complexas.

---

# **5. Propriedades essenciais do Document**

## **5.1 Estruturais**
```
document.documentElement   // <html>
document.head
document.body
document.forms
document.images
```

## **5.2 Estado do documento**
```
document.readyState   // "loading", "interactive", "complete"
document.visibilityState
document.hidden
```

## **5.3 Informações gerais**
```
document.title
document.URL
document.lastModified
document.referrer
```

---

# **6. Eventos do `document`**

O `document` é onde você ouve eventos relacionados ao estado da página.

### **DOM carregado**
```
document.addEventListener("DOMContentLoaded", () => {
  console.log("DOM pronto!");
});
```

### **Visibilidade**
```
document.addEventListener("visibilitychange", () => {
  if (document.hidden) console.log("Usuário trocou de aba");
});
```

### **Eventos de input no nível global**
```
document.addEventListener("keydown", ...)
document.addEventListener("click", ...)
```

---

# **7. Inserção, Remoção e Substituição via `document`**

Você manipula o DOM chamando métodos nos elementos,  
mas **quase sempre começa usando o document para encontrá-los**.

```
const btn = document.querySelector("#btn");
btn.remove();         // remove o nó
btn.replaceWith(...)  // troca
btn.before(...)       // insere antes
btn.after(...)        // insere depois
```

---

# **8. Templates e HTML Dinâmico**

Muito importante em UI builders (como seu editor dinâmico).

## **8.1 Criar DOM a partir de HTML**
```
const div = document.createElement("div");
div.innerHTML = "<span>algo</span>";
```

## **8.2 Criar fragmentos leves**
```
const tpl = document.createElement("template");
tpl.innerHTML = "<p>Item</p>";
document.body.append(tpl.content.cloneNode(true));
```

`template.content` é um DocumentFragment — perfeito para perfomance.

---

# **9. Busca e Leitura de Scripts, JSON e Tags**

O `document` permite pegar qualquer nó:

```
document.querySelector('script[type="application/json"]').textContent
```

Isso é essencial para seu:

- `loadJsonFromScript`
- `template-json`
- Configs de editor carregadas do DOM

---

# **10. Document como “orquestrador” geral da página**

O `document` também é responsável por:

### **10.1 Foco**
```
document.activeElement
```

### **10.2 Seleção de texto**
```
document.getSelection()
```

### **10.3 Execução de comandos**
(deprecated, mas ainda usado às vezes)
```
document.execCommand("copy")
```

### **10.4 Cookies**
```
document.cookie
```

### **10.5 Fullscreen API**
```
document.fullscreenElement
document.exitFullscreen()
```

---

# **11. Quando você deve trabalhar com `document`**

Usar `document` é recomendável quando você quer:

- Selecionar elementos existentes.
- Criar novos elementos.
- Acessar `<head>` ou `<body>`.
- Gerenciar scripts, estilos e templates.
- Ouvir eventos globais.
- Trabalhar com visibilidade, foco ou estado da página.

É literalmente a **raiz de tudo que existe no DOM**.

---

# **12. Outros objetos irmãos importantes**

Aprender o `document` naturalmente te leva a aprender:

- `window`
- `navigator`
- `location`
- `history`
- `screen`

Esses pertencem ao **BOM (Browser Object Model)**,  
que está no seu pedido e virá em outro glossário.

---

# **Resumo mental para lembrar para sempre**

**Document = a representação viva do HTML carregado.  
É a porta de entrada para criar, buscar e manipular tudo.  
Sem ele não existe DOM, não existe UI, não existe nada.**

---

# **Fim**
