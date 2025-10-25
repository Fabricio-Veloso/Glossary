# Lua Crash Course

## Table of Contents

- Comments
- Variables
- Control Flow
- Modules
- Functions
- Metatables
- Bonus :)

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

## Variables: Simple Literals

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

## Variables: Functions

```lua
local higher_order = function(value)
  return function(another)
    return value + another
  end
end

local add_one = higher_order(1)
print("add_one(2) -> ", add_one(2))
```

## Variables: Tables

Effectively, Lua's only data structure.

- Same structure is used for maps & lists

## Variables: Tables

As a list...

```lua
local list = { "first", 2, false, function() print("Fourth!") end }
print("Yup, 1-indexed:", list[1])
print("Fourth is 4...:", list[4]())
```

## Variables: Tables

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

## Variables: Not Covered

- Thread
- Userdata

## Control Flow: `for`

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

## Control Flow: `for`

```lua
local reading_scores = { teej_dv = 9.5, ThePrimeagen = "N/A" }
for key, value in pairs(reading_scores) do
  print(key, value)
end
```

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

## Modules

There isn't anything special about modules.
Modules are just files!

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

## Functions: Multiple Returns

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

## Functions: Multiple Returns

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

String Shorthand

```lua
local single_string = function(s)
  return s .. " - WOW!"
end

local x = single_string("hi")
local y = single_string "hi"
print(x, y)
```

## Functions: Calling

Table Shorthand

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

## Metatables

```lua
local vector_mt = {}
vector_mt.__add = function(left, right)
  return setmetatable({
    left[1] + right[1],
    left[2] + right[2],
    left[3] + right[3],
  }, vector_mt)
end

local v1 = setmetatable({ 3, 1, 5 }, vector_mt)
local v2 = setmetatable({ -3, 2, 2 }, vector_mt)
local v3 = v1 + v2
vim.print(v3[1], v3[2], v3[3])
vim.print(v3 + v3)
```

## Metatables

```lua
local fib_mt = {
  __index = function(self, key)
    if key < 2 then return 1 end
    -- Update the table, to save the intermediate results
    self[key] = self[key - 2] + self[key - 1]
    -- Return the result
    return self[key]
  end
}

local fib = setmetatable({}, fib_mt)

print(fib[5])
print(fib[1000])
```

## Metatables

Other notable fields:

- `__newindex(self, key, value)`
- `__call(self, ...)`

## Quick Neovim Goodies

```lua
vim.keymap.set("n", "<space><space>x", "<cmd>source %<CR>")
vim.keymap.set("n", "<space>x", ":.lua<CR>")
vim.keymap.set("v", "<space>x", ":lua<CR>")
```

## Quick Neovim Goodies

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
## 📦 Caminhos de Módulos e `package.path` no Lua
- O Lua possui um sistema simples para encontrar e carregar módulos externos, controlado pelas variáveis globais `package.path` e `package.cpath`.  Esses caminhos dizem ao interpretador **onde procurar os arquivos** quando usamos `require("modulo")`.

---
### 🧩 Entendendo o `package.path`

- O `package.path` é uma string que lista os diretórios onde o Lua procura arquivos `.lua`.  
- Por padrão, ele inclui caminhos como:
```
./?.lua
/usr/share/lua/5.4/?.lua
/usr/local/share/lua/5.4/?.lua
```

Mas se o projeto tem seus arquivos em subpastas (por exemplo `src/`), precisamos adicioná-las manualmente.
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
## 📦 Resumo:

- O require("calculadora") vai procurar por calculadora.lua nos diretórios listados em package.path.
 - Se o arquivo não estiver em um desses locais, Lua lança um erro: module 'calculadora' not found.
## 🧱 Adicionando múltiplos diretórios

Você pode concatenar vários diretórios no package.path:
```lua
package.path = package.path
  .. ";./src/?.lua"
  .. ";./lib/?.lua"
  .. ";./modules/?.lua"
```

- Assim o require funcionará com módulos espalhados em subpastas diferentes.
## ⚙️ package.cpath — módulos binários

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
## 📜 Listar argumentos passados via terminal
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
## 🕹️ Criar modo de desenvolvimento

```lua
local DEV_MODE = true

if DEV_MODE then
  print("Rodando em modo de desenvolvimento")
end
```
- Útil para habilitar logs, prints ou carregamentos adicionais só durante o desenvolvimento.
## 🧭 Depurar caminhos de busca

```lua
print("Caminhos de busca Lua:")
print(package.path)
```
- Permite verificar o que está realmente valendo em package.path e package.cpath.
## 📂 Estrutura recomendada de projeto Lua
meu-projeto/
├── main.lua
├── src/
│   ├── init.lua
│   └── calculadora.lua
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
## 🧰 Dicas rápidas

- ? → substituído pelo nome do módulo em require.
- ; → separa múltiplos caminhos.
- package.path → caminhos de módulos .lua.
- package.cpath → caminhos de módulos nativos (.so / .dll).
- debug.getinfo → ajuda a descobrir o diretório atual.
- arg → argumentos de linha de comando.
- init.lua → define um pacote de forma hierárquica.

## 💡 Exemplo completo e funcional
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
