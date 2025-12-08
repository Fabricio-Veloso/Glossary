# Lua Crash Course

## Table of Contents

- Comments
- Variables
- Control Flow
- Modules
- Functions
- Tables
- Metatables
- Neovim Goodies
- Vim dev tips

## Background Info

Lua is elegant

- Lua uses "Mechanisms over Policies"
- Lua is designed to be embedded
- Lua is cool

## Comments

```lua
-- This is a comment. It starts with two dashes

--[[ This is also
     a comment.

     But it spans multiple lines!
--]]
```

# Variables:

## Variables: Strings
```lua
local string = "hello, world"
local single = 'also works'
local crazy = [[ This
 is multi line and literal ]]
```

## Variables: Manipulação de strings

### `:find(pattern)`
Retorna **posição inicial e final** do padrão na string.

```lua
local s = "arquivo.lua"
local i, j = s:find("%.lua$")
-- i=8, j=11
```

---

### `:sub(i, j)`
Extrai substring com base em índices.

```lua
local s = "abcdef"
print(s:sub(2, 4))
-- "bcd"
```

---

### `:len()`
Retorna o tamanho da string.

```lua
print("opa":len())
-- 3
```

---

### `:format(...)`
Formatação ao estilo `printf`.

```lua
local nome, idade = "Fab", 28
print(("Olá %s (%d anos)"):format(nome, idade))
```

---

## Variables: `string.match` (ou `:match`)

Extrai partes específicas de uma string usando **patterns** nativos de Lua.

### Exemplo real
```lua
local module_path = f:match("lua/(.*)%.lua$")
```

**Interpretação do padrão:**
- `lua/` → procura esse prefixo literal  
- `(.*)` → captura “qualquer coisa”  
- `%.lua` → `.lua` (o `%` escapa o ponto)  
- `$` → fim da string

### Exemplo simples
```lua
local s = "nome: fab"
local value = s:match("nome:%s*(.*)")
print(value)  
-- fab
```

### Quando usar
- Extrair trechos de caminhos
- Buscar nomes, padrões simples
- Parsear strings em geral

---
## 🔹 Alternativas a `match`

### `string.find(pattern)`
Retorna apenas **posição inicial e final** da primeira ocorrência.

```lua
local s = "abc123"
local i, j = s:find("%d+")
-- i = 4, j = 6
```

Use quando:  
• você só quer saber *onde* algo aparece.  
• não precisa extrair o texto.

---

### `string.gmatch(pattern)`
Cria um **iterador** que percorre todas as ocorrências.

```lua
for num in ("a1b22c333"):gmatch("%d+") do
  print(num)
end
-- 1
-- 22
-- 333
```

Use quando:  
• precisa iterar peças de texto baseadas em padrões.  
• é o equivalente a “split com regex”.

---

## 3. `string.gsub` (ou `:gsub`)

Faz **substituição global** em uma string.

### Exemplo real
```lua
local dotted = caminho:gsub("/", ".")
```

Transforma paths do estilo `a/b/c` em `a.b.c`.

### Exemplo simples
```lua
local txt = "a-b-c"
local novo = txt:gsub("-", "_")
print(novo)
-- a_b_c
```

### Quando usar
- Normalizar textos
- Trocar separadores
- Gerar nomes de módulos
- Limpar ou uniformizar entradas

---
## 🔹 Alternativas a `gsub`

### `string.sub(i, j)`
Retorna pedaço da string.

```lua
local s = "abcdef"
print(s:sub(2,4)) -- bcd
```

Use quando:  
• já sabe as posições.  
• está usando `find` → pega posições → usa `sub`.

---

### `string.upper()` / `string.lower()`
Transforma caixa.

```lua
print("Fab":upper())
print("Fab":lower())
```

Use quando:  
• precisa normalizar entrada.  
• vai comparar strings.

---

## 3. Conversões e utilidades

### `type(x)`
Retorna o tipo primitivo (`string`, `number`, `table`, `function`, etc.).

---

### `tostring(x)` / `tonumber(x)`
Conversão explícita.

```lua
print(tostring(123))  -- "123"
print(tonumber("42")) -- 42
```

---

### `error(msg)`
Interrompe a execução com mensagem.

```lua
if not ok then error("Algo deu errado") end
```

---

### `assert(cond, msg?)`
Abreviação comum: falha caso cond seja falsa.

```lua
local f = assert(io.open("dados.txt", "r"))
```

---

### `pcall(fn)`
Executa uma função “protegida”, capturando qualquer erro sem quebrar o fluxo.

```lua
local ok, result = pcall(function()
  return arr[10].x
end)

if not ok then
  print("Erro capturado:", result)
end
```

---

## 4. Funções matemáticas úteis (`math.*`)

### `math.floor(x)`
Arredonda para baixo.

### `math.ceil(x)`
Arredonda para cima.

### `math.max(a, b, ...)`
Maior valor.

### `math.min(a, b, ...)`
Menor valor.

### `math.random(a, b)`
Número aleatório entre *a* e *b* (inclusive).

### `math.abs(x)`
Valor absoluto.

```lua
print(math.floor(2.9)) -- 2
print(math.random(1, 10))
```

---
## Variables Simple Literals

```lua
local number = 5

local string = "hello, world"
local single = 'also works'
local crazy = [[ This
 is multi line and literal ]]

local truth, lies = true, false

local nothing = nil
```

## Variables: Functions

```lua
local function hello(name)
  print("Hello!", name)
end

local greet = function(name)
  -- .. is string concatenation
  print("Greetings, " .. name .. "!")
end
```


```lua
local higher_order = function(value)
  return function(another)
    return value + another
  end
end

local add_one = higher_order(1)
print("add_one(2) -> ", add_one(2))
```

Effectively, Lua's only data structure.

- Same structure is used for maps & lists


As a list...

```lua
local list = { "first", 2, false, function() print("Fourth!") end }
print("Yup, 1-indexed:", list[1])
print("Fourth is 4...:", list[4]())
```
As a map...

```lua
local t = {
  literal_key = "a string",
  ["an expression"] = "also works",
  [function() end] = true
}

print("literal_key   : ", t.literal_key)
print("an expression : ", t["an expression"])
print("function() end: ", t[function() end])
```
## Control Flow

### Control Flow:`ipairs`

Itera **sequencialmente** sobre arrays numéricos (1,2,3,...).  
Para ao encontrar o primeiro índice nil.

- Retorna **índice** e **valor**.
- Ideal para listas bem formadas e ordenadas.

### Exemplo
```lua
local lista = { "a", "b", "c" }

for i, v in ipairs(lista) do
  print(i, v)
end
-- 1 a
-- 2 b
-- 3 c
```

### Quando usar
- Arrays numéricos
- Resultados de splits
- Listas compactas e contínuas
* Iterador que percorre **somente índices numéricos sequenciais** começando em `1`.
* Para automaticamente ao encontrar um valor `nil`.
* Útil para **listas** (arrays).
* Garante **ordem previsível**.

* Iterador genérico que percorre **todas as chaves** de uma tabela.
* **Não garante ordem**.
* Usado para dicionários, maps, objetos arbitrários.

## 🔹 Alternativas a `ipairs`

Use quando:  
• sua tabela não é um array puro.  
• você precisa inspecionar tudo sem se importar com ordem.

---

### `next(t)`
Função de baixo nível que `pairs` usa internamente.  
Retorna o **próximo** par chave/valor.

```lua
local t = { x = 1, y = 2 }
local k, v = next(t)
```

Use quando:  
• quer controle mais fino sobre iteração.  
• quer escrever seu próprio iterador.

---

### Control Flow: "_" como variável descartável

* `_` é **uma variável comum**, sem comportamento especial da linguagem.
* Usado por **convenção** quando você quer receber um valor mas **não precisa** dele.
* Em loops como:

```
for _, value in ipairs(tabela) do
...
end
```

… `_` indica ao leitor: **“ignora o valor desta variável, não é relevante aqui”**.

---
```lua
local favorite_accounts = { "teej_dv", "ThePrimeagen", "terminaldotshop" }
for index = 1, #favorite_accounts do
  print(index, favorite_accounts[index])
end

for index, value in ipairs(favorite_accounts) do
  print(index, value)
end
```

## Control Flow: `for`

```lua
local reading_scores = { teej_dv = 10, ThePrimeagen = "N/A" }
for index = 1, #reading_scores do
  print(reading_scores[index])
end
```

Doesn't Print Anything - the "length" of the array is 0.

We aren't using it as an array, we're using it as a map!


## Control Flow: `if`

```lua
local function action(loves_coffee)
  if loves_coffee then
    print("Check out `ssh terminal.shop` - it's cool!")
  else
    print("Check out `ssh terminal.shop` - it's still cool!")
  end
end

-- "falsey": nil, false
action() -- Same as: action(nil)
action(false)

-- Everything else is "truthy"
action(true)
action(0)
action({})
```

# Modules

## Modules:📦 Caminhos de Módulos e `package.path` no Lua
- O Lua possui um sistema simples para encontrar e carregar módulos externos, controlado pelas variáveis globais `package.path` e `package.cpath`.  Esses caminhos dizem ao interpretador **onde procurar os arquivos** quando usamos `require("modulo")`.

---
### Modules: 🧩 Entendendo o `package.path`

- O `package.path` é uma string que lista os diretórios onde o Lua procura arquivos `.lua`.  
- Por padrão, ele inclui caminhos como:
```
./?.lua
/usr/share/lua/5.4/?.lua
/usr/local/share/lua/5.4/?.lua
```
- Mas se o projeto tem seus arquivos em subpastas (por exemplo `src/`), precisamos adicioná-las manualmente.

---
### ⚙️ Exemplo básico

```lua
package.path = package.path .. ";./src/?.lua"

local calculadora = require("calculadora")
print(calculadora.somar(2, 3))
```

Explicação da linha:
- package.path → caminho de busca atual.
- .. → concatena strings em Lua.
- ";./src/?.lua" → adiciona a pasta src como caminho de busca adicional.
- ? → é um curinga substituído pelo nome do módulo (ex: calculadora → src/calculadora.lua).

### Modules: 📦 Explicação do exemplo básico:

- O require("calculadora") vai procurar por calculadora.lua nos diretórios listados em package.path.
 - Se o arquivo não estiver em um desses locais, Lua lança um erro: module 'calculadora' not found.

## Modules: 🧱 Adicionando múltiplos diretórios

Você pode concatenar vários diretórios no package.path:
```lua
package.path = package.path
  .. ";./src/?.lua"
  .. ";./lib/?.lua"
  .. ";./modules/?.lua"
```

- Assim o require funcionará com módulos espalhados em subpastas diferentes.

## Modules: ⚙️ package.cpath — módulos binários

- O package.cpath é o equivalente de package.path, mas serve para módulos nativos compilados (.so no Linux, .dll no Windows):
```lua
package.cpath = package.cpath .. ";./bin/?.so"
```
- Esse tipo de extensão é usada em bindings C ou bibliotecas externas.
	- 🧠 Informações úteis relacionadas
	- 🧭 Obter o diretório atual dinamicamente

```lua
local current_dir = debug.getinfo(1, "S").source:match("@(.*/)")
print("Diretório atual:", current_dir)
```
- Isso retorna o diretório onde o arquivo atual está sendo executado.
- Pode ser usado para ajustar o package.path de forma automática:
```lua
local dir = debug.getinfo(1, "S").source:match("@(.*/)")
package.path = package.path .. ";" .. dir .. "src/?.lua"
```

- Assim o Lua sempre encontra seus módulos mesmo se o script for executado de outro local.
---
## Modules: Quando `init.lua` é necessário

* Apenas quando você quer que **a pasta inteira seja tratada como módulo**, permitindo:

```
require("nome_da_pasta")
```

* Nesse caso, Lua procura automaticamente por:

```
nome_da_pasta/init.lua
```

Se não existir, o `require` falha.

## Modules: Quando `init.lua` NÃO é necessário

* Quando você importa **diretamente um arquivo específico**, como:

```
require("make.py-make.Identifyers-python.identify-django")
```

* Pastas intermediárias **não precisam ter init.lua**.
* Você pode importar arquivos de **qualquer nível**, desde que estejam dentro do `runtimepath`.
---
## Modules: Organização recomendada

- Use `init.lua` apenas quando quiser:
  - Agregar várias funções em uma interface limpa.
  - Criar um módulo “raiz” para facilitar imports.
- Para arquivos isolados, importe direto sem complicar a estrutura.

```lua
-- foo.lua
local M = {}
M.cool_function = function() end
return M
```

```lua
-- bar.lua
local foo = require('foo')
foo.cool_function()
```
## Modules: can export only the main Functions
- The secondary ones can't be used by the module that requires the exported module, but can use the principal flawlesly.

```lua
local M = {}

local function interna()
  print("sou privada")
end

function M.publica()
  interna()
end

return M
```



# Functions

## Functions: Multiple Returns

## exemple1
```lua
local returns_four_values = function()
  return 1, 2, 3, 4
end

first, second, last = returns_four_values()

print("first: ", first)
print("second:", second)
print("last:  ", last)
-- the `4` is discarded :'(
```

## exemple2

```lua
local variable_arguments = function(...)
  local arguments = { ... }
  for i, v in ipairs({...}) do print(i, v) end
  return unpack(arguments)
end

print("===================")
print("1:", variable_arguments("hello", "world", "!"))
print("===================")
print("2:", variable_arguments("hello", "world", "!"), "<lost>")
```

## Functions: Calling

### String Shorthand

```lua
local single_string = function(s)
  return s .. " - WOW!"
end

local x = single_string("hi")
local y = single_string "hi"
print(x, y)
```

### Table Shorthand

```lua
local setup = function(opts)
  if opts.default == nil then
    opts.default = 17
  end

  print(opts.default, opts.other)
end

setup { default = 12, other = false}
setup { other = true}
```

## Functions: Colon Functions

```lua
local MyTable = {}

function MyTable.something(self, ...) end
function MyTable:something(...) end
```
# Tables

## Tables: `table.insert`

Insere um valor no final de uma tabela tratada como lista.

### Exemplo real
```lua
table.insert(handlers, require(module_path))
```

### Exemplo simples
```lua
local t = {}
table.insert(t, "um")
table.insert(t, "dois")
-- t = { "um", "dois" }
```

### Quando usar
- Construir listas dinamicamente
- Acumular itens de processamento
- Montar arrays de resultados

---

## 5. Como tudo se conecta no seu código

```lua
for _, f in ipairs(files) do
  local module_path = f:match("lua/(.*)%.lua$"):gsub("/", ".")
  table.insert(modules, require(module_path))
end
```

**Pipeline:**
1. `ipairs(files)` → percorre arquivos encontrados  
2. `match("lua/(.*)%.lua$")` → extrai caminho interno  
3. `gsub("/", ".")` → converte para estilo `a.b.c`  
4. `table.insert(..., require(...))` → carrega e armazena módulo  

Simples, direto e idiomático.

---
## Tables: `table.insert(t, value)`
Adiciona um valor ao final de uma tabela tratada como lista.

```lua
local t = {1, 2}
table.insert(t, 3)
-- {1, 2, 3}
```

## Tables:🔹 Alternativas a `table.insert`

### `table.remove(t, index?)`
Remove um item.  
Sem índice → remove o último.

```lua
local t = {10, 20, 30}
table.remove(t, 2)
-- {10, 30}
```

---

### `table.move(src, f, e, dest, dst?)`
Move um intervalo de elementos entre tabelas.

```lua
local a = {1,2,3,4,5}
local b = {}
table.move(a, 2, 4, 1, b)
-- b = {2,3,4}
```

Use quando:  
• precisa “copiar” fatias.  
• quer performance maior que loops manuais.

---

### `table.sort(t, comp?)`
Ordenação com função opcional de comparação.

```lua
local t = {3,1,4}
table.sort(t)
-- {1,3,4}

table.sort(t, function(a,b)
  return a > b
end)
-- {4,3,1}
```

Use quando:  
• quer ordenar arrays.  
• quer ordenar por algum critério customizado.

---
---

## Tables: `table.remove(t, index?)`
Remove um elemento.  
Sem índice → remove o último.

```lua
local t = { "a", "b", "c" }
table.remove(t, 2)
-- { "a", "c" }
```

---

## Tables: `table.sort(t, comp?)`
Ordena a lista.  
Aceita função de comparação opcional.

```lua
local t = { 5, 1, 3 }
table.sort(t)
-- {1, 3, 5}

table.sort(t, function(a, b) return a > b end)
-- {5, 3, 1}
```

---

## Tables: `table.concat(t, sep?)`
Concatena todos os itens em uma única string.

```lua
local nomes = {"a", "b", "c"}
local s = table.concat(nomes, ", ")
-- "a, b, c"
```

---

## Tables: `pairs(t)`
Itera **todos** os campos de uma tabela, sem garantia de ordem.

```lua
for k, v in pairs(config) do
  print(k, v)
  end
  ```

  ---

  ## `ipairs(t)`
  Itera sequencialmente índices numéricos 1..n.  
  Útil para arrays “bem formados”.

```lua
  for i, v in ipairs(lista) do
    print(i, v)
    end
```

---

# Metatables :

## no contexto do Neovim  
Criando APIs elegantes e comportamentos “mágicos” de forma clara

Metatables permitem que você modifique o comportamento padrão de tabelas:  
• definir operadores (`+`, `-`, `..`)  
• interceptar leituras e escritas de campos  
• criar funções “que parecem objetos”  
• criar acesso dinâmico  
• implementar memoização, lazy loading, DSLs, etc.

No Neovim, isso é muito usado para criar **APIs mais bonitas**, do tipo:

```lua
api.buf(3).lines()
api.project("meu-projeto").files()
```

Essas APIs parecem objetos, mas são só tabelas com metatables.

---

## Metatables: 1. Exemplo simples e claro: criando uma API de buffer “bonita”

Suponha que você quer criar uma API onde você possa fazer:

```lua
local buf = MyAPI.buf(0)
print(buf:get_line(1))
```

Ou até:

```lua
MyAPI.buf(0):append("nova linha")
```

Vamos construir isso passo a passo com metatables.

---

## Metatables: 2. Estrutura básica com `__index`

Criamos uma tabela “classe” que contém os métodos.

```lua
local Buffer = {}

function Buffer:get_line(n)
  return vim.api.nvim_buf_get_lines(self.id, n-1, n, false)[1]
end

function Buffer:append(text)
  vim.api.nvim_buf_set_lines(self.id, -1, -1, false, { text })
end
```

Agora criamos o *metatable* que vai dizer:  
> quando tentarem acessar algo em um objeto `buf`, procure em `Buffer`.

```lua
local buffer_mt = {
  __index = Buffer,
}
```

Criamos um construtor:

```lua
local MyAPI = {}

function MyAPI.buf(id)
  return setmetatable({ id = id }, buffer_mt)
end

return MyAPI
```

Agora isso funciona:

```lua
local buf = MyAPI.buf(0)
print(buf:get_line(1))
buf:append("hello")
```

**Por quê funciona?**  
Porque `buf` não tem `get_line`, mas seu metatable tem `__index = Buffer`, então Lua usa aquele método.

---

## Metatables: 3. Exemplo mais avançado: carregamento dinâmico de módulos (tipo “lazy API”)

Muito útil em plugins onde você quer:

```lua
local api = require("meuplugin")
api.fs.read("file.txt")
api.fs.write("file.txt", "conteúdo")
```

Mas você não quer que `api.fs` seja uma tabela estática.  
Você quer que **ao acessar `api.fs` pela primeira vez**, ele carregue o módulo `meuplugin.fs`.

Use `__index` dinamicamente:

```lua
local api = {}
local api_mt = {}

api_mt.__index = function(self, key)
  -- Carrega módulo on-demand
  local mod = require("meuplugin." .. key)
  -- Cacheia para futuras chamadas
  rawset(self, key, mod)
  return mod
end

return setmetatable(api, api_mt)
```

Agora a API é “mágica” e você só cria arquivos conforme precisa.

---

## Metatables: 4. Exemplo de operador customizado em API (útil para DSLs)

Digamos que você está criando uma API que monta comandos:

```lua
local cmd = Cmd("git") + "status" + "-sb"
vim.print(cmd())
```

Podemos fazer isso assim:

```lua
local Cmd = {}
local cmd_mt = {}

function cmd_mt.__call(self)
  return vim.fn.system(self.args)
end

function cmd_mt.__add(self, arg)
  local new = { args = {} }
  for _, v in ipairs(self.args) do table.insert(new.args, v) end
  table.insert(new.args, arg)
  return setmetatable(new, cmd_mt)
end

function Cmd:new(base)
  return setmetatable({ args = { base } }, cmd_mt)
end

return function(base)
  return Cmd:new(base)
end
```

Você acabou de criar um mini-DSL usando operadores.

---

## Metatables: 5. Campos úteis de metatables (resumo limpo)

Campo | Para quê serve | Exemplo prático
----- | -------------- | ----------------
`__index` | Delegar leitura | procurar métodos “da classe”
`__newindex` | Interceptar escrita | validar campos, impedir ou logar
`__call` | Transformar tabela em função | DSLs, wrappers, helpers
`__add`, `__sub`, etc. | Definir operadores | criar mini linguagens, estruturas
`__tostring` | Controlar saída | logs bonitos no Neovim
`__metatable` | Proteger metatable | esconder implementação

---

## Metatables: 6. Um exemplo “muito real de plugin”: API fluente para arquivos

Imagine uma API onde você pode fazer:

```lua
local f = FS("notes/todo.md")
print(f:size())
print(f:text())
```

Implementação:

```lua
local FS = {}
local fs_mt = {}

function FS:size()
  return vim.loop.fs_stat(self.path).size
end

function FS:text()
  local fd = assert(vim.loop.fs_open(self.path, "r", 438))
  local stat = assert(vim.loop.fs_fstat(fd))
  local data = assert(vim.loop.fs_read(fd, stat.size, 0))
  vim.loop.fs_close(fd)
  return data
end

fs_mt.__index = FS

return function(path)
  return setmetatable({ path = path }, fs_mt)
end
```

Pronto:  
API fluida, natural, elegante — e 100% baseada em metatables.

---

## Metatables: Conclusão rápida

Metatables servem para:

- Criar APIs estilo “objeto”
- Interceptar métodos dinamicamente
- Criar lazy loaders e DSLs
- Adicionar operadores customizados
- Construir estruturas mais naturais para plugins

E o melhor: **Você pode transformar praticamente qualquer tabela em uma API rica e agradável de usar no Neovim.**

---
# Neovim Goodies

## Neovim Goodies: Chamando funções Vimscript: `vim.fn.*`

Permite usar qualquer função do Vimscript diretamente no Lua.

### `vim.fn.glob(pattern)`
Busca arquivos e retorna string com caminhos separados por newline.

```lua
local arquivos = vim.fn.glob("lua/**/*.lua")
```

---

### `vim.fn.globpath(path, pattern, nosuf, list)`
Busca arquivos em **vários** diretórios.

```lua
local paths = vim.fn.globpath(vim.o.runtimepath, "plugin/*.lua", 0, 1)
```

---

### `vim.fn.stdpath("config" | "data")`
Paths padrão do Neovim.

```lua
local config = vim.fn.stdpath("config") -- ~/.config/nvim
```

---

### `vim.fn.getcwd()`
Diretório atual.

---

### `vim.fn.system(cmd)` / `vim.fn.systemlist(cmd)`
Executa comandos externos.

```lua
local out = vim.fn.system("ls")
local lines = vim.fn.systemlist("ls")
```

---

### `vim.fn.expand("%")`
Retorna o arquivo atual do buffer.

```lua
local atual = vim.fn.expand("%")
```

---

## Neovim Goodies: API nativa do editor: `vim.api.*`

A API mais robusta e segura para manipular buffers, janelas e o editor.

### `nvim_get_current_buf()`
ID do buffer atual.

```lua
local buf = vim.api.nvim_get_current_buf()
```

---

### `nvim_buf_get_lines(buf, start, end_, strict)`
Obtém linhas do buffer.

```lua
local linhas = vim.api.nvim_buf_get_lines(buf, 0, -1, false)
```

---

### `nvim_buf_set_lines(buf, start, end_, strict, linhas)`
Escreve linhas no buffer.

```lua
vim.api.nvim_buf_set_lines(buf, 0, 0, false, { "primeira linha" })
```

---

### `nvim_set_keymap(mode, lhs, rhs, opts)`
Cria keymaps.

```lua
vim.api.nvim_set_keymap("n", "<leader>x", ":echo 'oi'<CR>", { noremap = true })
```

---

### `nvim_create_autocmd(event, opts)`
Criar autocmds é essencial para plugins.

```lua
vim.api.nvim_create_autocmd("BufWritePost", {
  pattern = "*.lua",
  callback = function() print("salvo!") end,
})
```

---

## Neovim Goodies: Utilitários gerais do Neovim: `vim.*`

### `vim.inspect(obj)`
Transforma tabelas em strings legíveis (debug).

```lua
print(vim.inspect({a=1, b=2}))
```

---

### `vim.deepcopy(t)`
Cópia profunda.

---

### `vim.tbl_islist(t)`
Retorna `true` se a tabela for array 1..n.

---

### `vim.tbl_deep_extend("force", t1, t2)`
Mescla tabelas profundamente.

```lua
local cfg = vim.tbl_deep_extend("force", defaults, user)
```

---

### `vim.schedule(fn)`
Executa no próximo tick da UI  
→ evita mexer no buffer durante eventos sensíveis.

```lua
vim.schedule(function()
  print("executado depois")
end)
```

---

## Neovim Goodies: Libuv exposta pelo Neovim: `vim.loop`

Ferramentas assíncronas de filesystem e processos.

### `vim.loop.fs_stat(path)`
Retorna info do caminho.

```lua
local st = vim.loop.fs_stat("init.lua")
```

---

### `vim.loop.fs_scandir(path)`
Escaneia diretórios.

```lua
local iter = vim.loop.fs_scandir(".")
local nome = vim.loop.fs_scandir_next(iter)
```

---

### `vim.loop.spawn(cmd, opts, callback)`
Executa comando externo assíncrono.

```lua
vim.loop.spawn("ls", { args = {} }, function()
  print("comando finalizou")
end)
```

---
```lua
vim.keymap.set("n", "<space><space>x", "<cmd>source %<CR>")
vim.keymap.set("n", "<space>x", ":.lua<CR>")
vim.keymap.set("v", "<space>x", ":lua<CR>")
```


```lua
-- Highlight when yanking (copying) text
--  Try it with `yap` in normal mode
--  See `:help vim.highlight.on_yank()`
vim.api.nvim_create_autocmd('TextYankPost', {
  desc = 'Highlight when yanking (copying) text',
  group = vim.api.nvim_create_augroup('kickstart-highlight-yank', { clear = true }),
  callback = function()
    vim.highlight.on_yank()
  end,
})
```
---
## Neovim Goodies:📜 Listar argumentos passados via terminal
```lua
for i, arg in ipairs(arg) do
  print("Arg", i, "=", arg)
end
```
- Permite rodar scripts com argumentos:

```lua
lua main.lua 10 20
```
E dentro do script acessar arg[1], arg[2], etc.
## Neovim Goodies:🕹️ Criar modo de desenvolvimento

```lua
local DEV_MODE = true

if DEV_MODE then
  print("Rodando em modo de desenvolvimento")
end
```
- Útil para habilitar logs, prints ou carregamentos adicionais só durante o desenvolvimento.
## Neovim Goodies: 🧭 Depurar caminhos de busca

```lua
print("Caminhos de busca Lua:")
print(package.path)
```
- Permite verificar o que está realmente valendo em package.path e package.cpath.
## Neovim Goodies: 📂 Estrutura recomendada de projeto Lua
meu-projeto/

├── main.lua

├── src/

│-----├── init.lua

│-----└── calculadora.lua

└── README.md

- main.lua: ponto de entrada.
- src/: contém os módulos do projeto.
- init.lua: arquivo especial que o Lua carrega automaticamente quando você faz require("src").

Exemplo:

```lua
-- src/init.lua
local calculadora = require("src.calculadora")

local M = {}
M.calc = calculadora
return M
```
E no main.lua:

```lua
package.path = package.path .. ";./src/?.lua;./src/?/init.lua"

local src = require("src")
print(src.calc.somar(5, 7))
```
- O Lua entende init.lua como o “ponto de entrada” de um módulo ou pacote — semelhante ao __init__.py no Python.

##  Neovim Goodies: 🧰 Dicas rápidas

- ? → substituído pelo nome do módulo em require.
- ; → separa múltiplos caminhos.
- package.path → caminhos de módulos .lua.
- package.cpath → caminhos de módulos nativos (.so / .dll).
- debug.getinfo → ajuda a descobrir o diretório atual.
- arg → argumentos de linha de comando.
- init.lua → define um pacote de forma hierárquica.

##  Neovim Goodies: 💡 Exemplo completo e funcional
Estrutura:

aprendendo-lua/
├── main.lua
└── src/
    └── calculadora.lua

```lua
src/calculadora.lua:

local calculadora = {}

function calculadora.somar(a, b)
  return a + b
end

function calculadora.subtrair(a, b)
  return a - b
end

return calculadora

main.lua:

package.path = package.path .. ";./src/?.lua"

local calculadora = require("calculadora")

print("=== Testando Calculadora ===")
print("Soma 5 + 3 =", calculadora.somar(5, 3))
print("Subtração 10 - 4 =", calculadora.subtrair(10, 4))
```
- Execução:
```
lua main.lua
```

- Saída esperada:
```
=== Testando Calculadora ===
Soma 5 + 3 = 8
Subtração 10 - 4 = 6
```
✅ Resumo final:
- Use package.path para apontar onde estão seus módulos .lua.
- Use package.cpath para módulos compilados (.so / .dll).
- O ? é substituído automaticamente pelo nome do módulo no require.
- init.lua transforma pastas em pacotes reutilizáveis.
- Você pode usar debug.getinfo para ajustar caminhos dinamicamente.
- Sempre verifique o package.path se o require não encontrar o módulo.

# Vim dev tips:

```lua
## seach paths
local files = vim.fn.globpath(vim.fn.stdpath("config") .. "/lua/make/make-folders/py-make/identifyers-python", "*.lua", false, true)
 ```
 - isso retorna algo como:
\´´´

## Vim dev tips: globpath(path, expr, nosuf?, list?, allinks?)
- Exemplo usado:

\´´´
local files = vim.fn.globpath(
vim.fn.stdpath("config") .. "/lua/make/make-folders/py-make/identifyers-python",
"*.lua",
false,
true
)
\´´´

#### Explicação dos parâmetros
##### 1) path

Diretório (ou lista de diretórios separados por vírgula) onde a busca será feita.

No exemplo:
```lua
vim.fn.stdpath("config") .. "/lua/make/make-folders/py-make/identifyers-python"
```
Isso vira algo como:

```lua
~/.config/nvim/lua/make/make-folders/py-make/identifyers-python
```

##### 2) expr

Padrão de busca (globbing).

    No exemplo: "*.lua" → todos os arquivos .lua.

#### 3) nosuf

Controla o uso das opções 'suffixes' e 'wildignore'.

- false → considere essas opções (comportamento comum)

- true → ignore 'suffixes' e 'wildignore'

- Normalmente você deixa false.

##### 4) list

- Define o formato do retorno:

- false → retorna string com caminhos separados por \n

- true → retorna lista Lua ({ "a.lua", "b.lua", ... })

- No exemplo: true → retorno é uma lista de arquivos.

#### 5) allinks

Mesmo papel do parâmetro em glob().
Controla se links simbólicos devem ser seguidos. Não usado no exemplo.

#### Por fim o resultado seria:
```lua
{
    "/caminho/a.lua",
    "/caminho/b.lua",
    "/caminho/c.lua",
}

```

## Vim dev tips: Entrada e saída (uso raro em ambientes como Neovim)

### `io.open(path, mode)`
Abre arquivo.

### `io.read()`
Lê da entrada padrão.

### `io.write()`
Escreve sem quebra de linha.

```lua
local f = io.open("log.txt", "w")
f:write("Oi!\n")
f:close()
```

Outras utilidades do SO:

- `os.rename`
- `os.remove`
- `os.time`
- `os.date`

Em Neovim, isso costuma ser substituído por APIs assíncronas (`vim.loop`, `vim.fs`, etc.).

---





