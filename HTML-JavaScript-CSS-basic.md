
# 📘 Glossário Rápido – HTML + CSS + JavaScript (Básico e Integrado)

> **Objetivo:** relembrar rápido *como pensar* e *como montar* interfaces Web usando HTML, CSS e JavaScript juntos — sem travar em detalhes básicos.

---

## 1. 🧱 Como o “Tripé da Web” funciona junto

### **HTML → estrutura**  
É a “base física” da página.  
Equivalente a: *paredes, portas, janelas*.

### **CSS → aparência**  
Controla visual, cores, posicionamento, espaçamento.  
Equivalente a: *pintura, decoração, móveis*.

### **JavaScript → comportamento**  
Manipula eventos, dados, animações, interações.  
Equivalente a: *eletricidade, automação, sensores*.

### **Fluxo mental básico**
1. **HTML**: crie *algo* na página  
2. **CSS**: estilize do jeito que quer  
3. **JS**: faça responder a eventos e lógica  

---

## 2. 📄 Estrutura mínima de um arquivo HTML integrado

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Exemplo</title>
    <link rel="stylesheet" href="styles.css">   <!-- CSS -->
</head>
<body>

    <div id="caixa">Olá!</div>  <!-- HTML -->

    <script src="script.js"></script>          <!-- JS -->
</body>
</html>
```

---

## 3. 🧱 Tabela rápida — HTML básico mais usado

| Elemento | Para que serve | Exemplo |
|---------|-----------------|---------|
| `<div>` | Contêiner genérico | `"<div>..."` |
| `<span>` | Texto inline | `"<span>..."` |
| `<img>` | Imagem | `<img src="">` |
| `<a>` | Link | `<a href="">` |
| `<p>` | Parágrafo | `<p>` |
| `<h1>`..`<h6>` | Títulos | `<h1>` |
| `<ul>`/`<li>` | Lista | `<ul><li>` |
| `<button>` | Botão | `<button>` |
| `<input>` | Campo | `<input type="text">` |
| `<form>` | Formulário | `<form>` |
| `<label>` | Rótulo | `<label for="">` |

### **Atributos comuns**  
| Atributo | Uso |
|----------|-----|
| `id=""` | Identificação única (JS/CSS) |
| `class=""` | Agrupar estilos e comportamentos |
| `src=""` | Imagens, scripts |
| `href=""` | Links |
| `type=""` | Tipo de input ou script |
| `data-*=""` | Valores customizados para JS |

---

## 4. 🎨 Tabela rápida — CSS básico mais usado

| Propriedade | Para que serve | Exemplo |
|-------------|-----------------|---------|
| `color` | Cor do texto | `color:red;` |
| `background` | Fundo | `background:#333;` |
| `width` / `height` | Tamanho | `width:100px;` |
| `margin` | Espaço externo | `margin:10px;` |
| `padding` | Espaço interno | `padding:10px;` |
| `border` | Borda | `border:1px solid` |
| `display` | Comportamento visual | `display:flex;` |
| `position` | Controle de posição | `position:absolute;` |
| `top/left/right/bottom` | Ajuste fino | `top:20px;` |
| `font-size` | Tamanho da fonte | `font-size:16px;` |
| `z-index` | Ordem de sobreposição | `z-index:10;` |

### **Seletores úteis**
| Seletor | Uso |
|---------|-----|
| `#id` | Um único elemento |
| `.classe` | Elementos com a classe |
| `elemento` | Todos os elementos desse tipo |
| `elemento elemento` | Descendentes |
| `elemento > filho` | Filhos diretos |

Exemplo rápido:
```css
#caixa { background: #222; color: white; }
.botao { padding: 10px; }
```

---

## 5. ⚙️ Tabela rápida — JavaScript básico mais usado

### **Selecionar elementos**
| Comando | Descrição |
|---------|------------|
| `document.getElementById()` | Mais simples e rápido |
| `document.querySelector()` | Um elemento (CSS-like) |
| `document.querySelectorAll()` | Vários elementos |

### **Eventos**
| Exemplo | Uso |
|---------|-----|
| `element.onclick = () => {}` | Clique simples |
| `element.addEventListener('click', fn)` | Recomendada |
| `drag`, `input`, `change`, `keyup`, etc | Eventos comuns |

### **Manipular conteúdo**
| Ação | Exemplo |
|------|---------|
| Ler texto | `el.textContent` |
| Alterar texto | `el.textContent = "novo"` |
| Alterar HTML | `el.innerHTML = "<b>Oi</b>"` |
| Alterar estilo | `el.style.left = "20px"` |
| Alterar atributos | `el.setAttribute("src", "...")` |

### **Exemplo mínimo de comportamento**
```js
const caixa = document.getElementById("caixa");

caixa.addEventListener("click", () => {
    caixa.style.background = "blue";
});
```

---

## 6. 🔗 Como HTML, CSS e JS conversam entre si (na prática)

### **Fluxo recomendado (mental e técnico)**

1. **Crie o elemento no HTML**
```html
<button id="botao-alterar">Trocar cor</button>
<div id="caixa"></div>
```

2. **Estilize no CSS**
```css
#caixa {
    width: 100px;
    height: 100px;
    background: red;
}
```

3. **Dê comportamento no JS**
```js
document.getElementById("botao-alterar")
    .addEventListener("click", () => {
        document.getElementById("caixa").style.background = "green";
    });
```

---

## 7. 🧲 “Ferramentas mentais” — transformando ideia em código

Essa seção é para te ajudar a ter um **mapeamento mental rápido**:

| Quero fazer… | Eu penso em… | E uso… |
|--------------|---------------|---------|
| Mostrar algo na tela | estrutura | HTML |
| Mudar aparência | cor, posição, layout | CSS |
| Reagir a ação do usuário | eventos | JS |
| Ler valor de um input | DOM | JS |
| Trocar texto/imagem | DOM | JS |
| Esconder / Mostrar | `display` | CSS (via JS) |
| Alinhar coisas | layout | CSS (flex/grid) |
| Deixar arrastável | mouse/touch | JS |
| Conectar dados no template Django | variáveis, loops | HTML + Django Template |
| Enviar algo para o backend | forms, fetch | HTML + JS |

---

## 8. 📚 Padrões que valem lembrar

### **JavaScript sempre chama o HTML via `id` ou `class`**
Se vai manipular algo → sempre dê `id` ou `class`.

### **CSS sempre estiliza usando `#id`, `.classe` ou nome de tag**
Mudar visual? Nunca pelo JS (a não ser em interações).

### **Separar arquivos é sempre melhor**
- `index.html`
- `styles.css`
- `script.js`

### **Em templates Django**, lembre de:
```html
{% load static %}
<link rel="stylesheet" href="{% static 'css/styles.css' %}">
<script src="{% static 'js/script.js' %}"></script>
```

---

## 9. 🛠️ Mini-exemplos prontos para lembrar quando bater dúvida

### **Alterar posição com JS**
```js
element.style.left = "100px";
element.style.top = "50px";
```

### **Ler valor de um input**
```js
const nome = document.getElementById("campo-nome").value;
```

### **Criar elemento dinamicamente**
```js
const div = document.createElement("div");
div.textContent = "Novo";
document.body.appendChild(div);
```

### **Loop simples sobre elementos**
```js
document.querySelectorAll(".item").forEach(el => {
    el.style.color = "red";
});
```

---

## 10. 🧭 Checklist mental para não travar quando estiver desenvolvendo

1. **O que eu quero criar existe como HTML?**  
2. **O visual disso já existe como CSS?**  
3. **Preciso reagir a algo? → JS.**  
4. **O JS tem a referência do elemento? (id/class)**  
5. **Estou criando ou só manipulando?**  
6. **Isso é estático ou precisa ser dinâmico?**  
7. **Isso deveria ser estilizado via CSS e não JS?**  
8. **Forma mais simples primeiro → melhorar depois.**

---

## 11. 🎯 Conclusão

Esse glossário serve para:

- lembrar como o tripé trabalha junto,  
- ter uma referência rápida de elementos comuns,  
- destravar raciocínio quando estiver programando,  
- dar segurança para implementar telas no Django,  
- te ajudar a fazer a ponte entre **“ideia → código”**.

Se quiser melhorar, dividir, aprofundar ou expandir — é só pedir.
