
# Glossário — DOM, CSSOM e Acesso a Estilos

Este glossário resume os conceitos essenciais para manipular elementos, textos e estilos no DOM, explicando por que certas propriedades funcionam e outras não.

---

## 1. **DOM (Document Object Model)**

É a representação estrutural do HTML enquanto o navegador roda.
Cada tag vira um **Node**, que pode ser:

* Element Node (`<div>`, `<span>`, `<p>`…)
* Text Node (conteúdo puro dentro de um elemento)
* Comment Node
* Document Node

### Pontos importantes:

* `element.textContent` devolve **somente texto**, nunca um elemento.
* Para acessar o `<span>` dentro de um `<div>`, sempre use seletores:

```
const span = div.querySelector('.text-content');
```

---

## 2. **CSSOM (CSS Object Model)**

É a árvore que representa os estilos finais de cada elemento.
O navegador junta:

* estilos inline (`style=""`)
* classes CSS
* heranças
* estilos do user-agent
* variáveis CSS

E gera o **estilo computado**.

### Acesso aos estilos:

* **Inline:**

```
element.style.fontSize
element.style.color
```

* **Todos inline (iterando):**

```
for (const prop of element.style) {
  console.log(prop, element.style[prop]);
}
```

* **Estilo computado (final real que aparece):**

```
const computed = getComputedStyle(element);
console.log(computed.fontSize);
```

---

## 3. **Diferença entre Inline Style e Computed Style**

### Inline Style (`element.style`)

* Só contém declarações escritas diretamente no atributo HTML.
* Exemplo:

```
<span style="font-size: 20px; color: red;">
```

* Acessível via:

```
span.style.fontSize  // "20px"
span.style.color     // "red"
```

### Computed Style (`getComputedStyle(element)`)

* Mostra o valor FINAL, após aplicar:

  * CSS externo
  * classes
  * variáveis CSS
  * heranças
  * estilos padrão do navegador
* Útil para saber o que realmente aparece na tela.

---

## 4. **Por que ****`textContent.fontSize`**** não existe?**

Porque:

* `element.textContent` → **string**
* strings não possuem estilos
* estilos pertencem ao **elemento**, não ao texto puro

Para acessar o estilo do `<span>` que contém o texto:

```
const span = element.querySelector('.text-content');
span.style.fontSize;
```

---

## 5. **Selecionando e navegando entre elementos**

### Seleção básica:

```
const el = document.getElementById('Text-Info');
```

### Selecionar filho `<span>`:

```
const span = el.querySelector('.text-content');
```

### Acessar todos os estilos inline desse `<span>`:

```
for (const prop of span.style) {
  console.log(prop, span.style[prop]);
}
```

---

## 6. **Text Node vs Element Node**

* **Element Node** → tem estilos (`style`, `classList`, eventos…)
* **Text Node** → é só texto bruto, sem propriedades visuais

Usar `textContent` sempre retorna **apenas o texto**, nunca o elemento:

```
div.textContent  // "concluiu o evento..."
div.textContent.style  // ❌ erro
```

Para alterar o estilo, você sempre precisa de um **elemento de verdade**, não de texto.

---

## 7. **Conceito central**

Quando se fala em manipular estilos de um elemento HTML **via JavaScript**, estamos falando de:

### **Manipulação do CSSOM**

Que pode ocorrer de duas formas:

* via `element.style` (inline)
* via `getComputedStyle()` (computado)

---

## 8. **Resumo essencial**

* DOM ⇢ estrutura dos elementos
* CSSOM ⇢ estrutura dos estilos
* `textContent` = texto → **não tem estilo**
* para acessar estilos, você precisa de um **element node**
* estilos ficam em `element.style` ou em `getComputedStyle(element)`

---

Se quiser, posso gerar também um glossário complementar sobre **manipulação de atributos**, **dataset**, **navegação DOM**, ou **boas práticas para lidar com elementos estilizados dinamicamente**.
