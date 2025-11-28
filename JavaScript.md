

# Glossário de JavaScript — Object, Map e Set

Este glossário oferece uma visão clara e prática dos principais recursos de `Object`, `Map` e `Set`.  
Focado no uso moderno do JavaScript e especialmente útil para manipulação dinâmica de configurações, edição de elementos e criação de sistemas reativos simples.

---

# 1. `Object` – A Base de Tudo

`Object` é o tipo fundamental para estruturas de dados do JavaScript.  
Todo objeto simples `{}` herda dele, e ele fornece métodos extremamente úteis para manipulação estrutural.

---

## 1.1 `Object.keys(obj)`
Retorna um array contendo **todas as chaves** do objeto.

```
Object.keys({ a: 1, b: 2 });  
// ["a", "b"]
```

**Quando usar:** iterar sobre chaves, validar propriedades, contar campos.

---

## 1.2 `Object.values(obj)`
Retorna um array contendo **todos os valores**.

```
Object.values({ a: 1, b: 2 });
// [1, 2]
```

**Quando usar:** análises nos valores, map/filter apenas nos valores.

---

## 1.3 `Object.entries(obj)`
Retorna pares `[chave, valor]`.

```
Object.entries({ a: 1, b: 2 });
// [["a", 1], ["b", 2]]
```

**Quando usar:** cadastro dinâmico, transformação de dados, criação de inputs dinâmicos.

---

## 1.4 `Object.fromEntries(array)`
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

## 1.5 `Object.assign(target, ...sources)`
Copia propriedades de outros objetos para o alvo.

```
const merged = Object.assign({}, defaults, userConfig);
```

**Quando usar:** merges rasos, aplicar defaults, sobrescrever configs.

---

## 1.6 `Object.freeze(obj)`
Torna o objeto totalmente imutável.

```
const cfg = Object.freeze({ theme: "dark" });
```

**Quando usar:** constantes, configs estáveis.

---

## 1.7 `Object.seal(obj)`
Impede adicionar/remover chaves, mas permite alterar valores existentes.

**Quando usar:** estruturas fixas com valores variáveis.

---

## 1.8 `Object.getOwnPropertyDescriptors(obj)`
Retorna detalhes completos sobre cada propriedade.

```
Object.getOwnPropertyDescriptors({ a: 1 });
```

**Quando usar:** sistemas reativos, clones profundos, proxies, validação profunda.

---

# 2. `Map` – Tabelas de Chave → Valor Modernas

`Map` é uma estrutura mais poderosa do que objetos simples quando a chave **não** é apenas texto.

---

## 2.1 Características principais

- aceita *qualquer* tipo de chave (strings, números, objetos, funções, elementos DOM)
- preserva a ordem de inserção
- fácil de iterar
- não tem colisões de propriedades (como `toString`)

---

## 2.2 Exemplo básico

```
const map = new Map();
map.set("fontSize", 22);
map.set(domElement, { x: 10, y: 20 });

map.get("fontSize"); // 22
map.get(domElement); // { x: 10, y: 20 }
```

---

## 2.3 Quando usar `Map`

- configs associadas a elementos DOM
- caching
- registrar componentes criados dinamicamente
- evitar colisão de nomes em objetos simples
- chave precisa ser um objeto (ex.: o próprio elemento HTML selecionado)

---

# 3. `WeakMap` – Chaves Fracas Associadas a Objetos

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

# 4. `Set` – Coleção de Valores Únicos

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

# 5. Diferença Geral entre Object, Map e Set

| Estrutura | Chaves | Ordem | Aceita objeto como chave? | Principal uso |
|----------|--------|--------|----------------------------|----------------|
| Object | strings/símbolos | geralmente sim | não | dados estáticos, configs simples |
| Map | qualquer coisa | sim | sim | tabelas dinâmicas, chaves complexas |
| WeakMap | objetos | sim | **somente objetos** | metadados ligados ao DOM |
| Set | valores únicos | sim | — | coleções sem duplicados |

---

# 6. Dicas para Editor de Layout (caso de uso real)

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

# 7. Referência rápida (cola fácil)

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

Fim do glossário.

