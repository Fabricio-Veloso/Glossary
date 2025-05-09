# 📐 Visual Block Mode no Neovim (`Ctrl+q` ou `Ctrl+v`)

## Ativando

- `Ctrl + q` (ou `Ctrl + v`) → entra em modo VISUAL BLOCK (`-- VISUAL BLOCK --` aparece)
- Use `j/k/h/l` para expandir a seleção por linhas ou colunas.

## Comandos úteis

### 🛠 Inserção múltipla

- `I` + texto + `Esc`: adiciona texto **no início de todas as linhas**
- `A` + texto + `Esc`: adiciona texto **no final de todas as linhas**

> Exemplo: adicionar `#` no início de várias linhas
>
> 1. `Ctrl+q`
> 2. `j` para selecionar várias linhas
> 3. `I# ` + `Esc`

### 🔄 Substituições com Regex

- `:'<,'>s/padrão/substituto/` → substitui nas linhas selecionadas
- Use `\v` para regex “normal” estilo moderno

#### Exemplos:

- `:'<,'>s/^/# ` → comenta linhas
- `:'<,'>s/_debug$//` → remove `_debug` do fim das linhas

### 🔍 Dicas de regex úteis

| Padrão | Significado              |
| ------ | ------------------------ |
| `^`    | Início da linha          |
| `$`    | Fim da linha             |
| `.*`   | Qualquer coisa           |
| `\v`   | Ativa modo regex “fácil” |
| `\0`   | Match completo           |

### 💡 Observações

- Pressione `Esc` **só depois de digitar o que deseja** em `I`/`A`
- Em `Visual Block`, `i` e `a` (minúsculos) não têm efeito
