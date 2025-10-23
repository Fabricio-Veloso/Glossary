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

# 🔍 Dicas de Regex e Substituição no Neovim

> 💡 Use `\v` no início do padrão para ativar o *modo “very magic”*, que torna os regex mais simples e parecidos com os de linguagens modernas.

---

## 🧩 Símbolos básicos de regex

| Símbolo | Nome | Significado / Uso | Exemplo | Resultado |
|----------|------|------------------|----------|------------|
| `^` | Início da linha | Faz o padrão casar **somente se começar no início da linha** | `:%s/^/# /` | Adiciona `# ` no início de cada linha |
| `$` | Fim da linha | Casa **somente o final da linha** | `:%s/.$/;/` | Substitui o último caractere da linha por `;` |
| `.` | Qualquer caractere | Representa **qualquer caractere único**, exceto `\n` | `/h.t/` | Casa “hat”, “hot”, “hit” etc. |
| `*` | Quantificador (0 ou mais) | Repete o padrão anterior **zero ou mais vezes** | `/ba*/` | Casa “b”, “ba”, “baa”, “baaa”... |
| `+` | Quantificador (1 ou mais) | Repete o padrão anterior **uma ou mais vezes** | `/ba+/` | Casa “ba”, “baa”, “baaa”, mas não “b” |
| `?` | Opcional | Padrão anterior **pode ou não aparecer** | `/colou?r/` | Casa “color” e “colour” |
| `[]` | Classe de caracteres | Lista de caracteres aceitos | `/[aeiou]/` | Casa qualquer vogal |
| `[^]` | Negação | Casa tudo **exceto** o que está dentro dos colchetes | `/[^0-9]/` | Casa qualquer caractere que **não** seja número |
| `()` | Grupo de captura | Agrupa parte do padrão para referenciar depois (`\1`, `\2`...) | `:%s/\v(ha)+/haha/` | Substitui “hahaha” por “haha” |
| `\1`, `\2` | Referência de captura | Reutiliza o conteúdo de um grupo capturado | `:%s/\v^([^,]+),([^,]+)/\2,\1/` | Inverte duas colunas CSV |
| `\0` | Match completo | Refere-se a **todo o texto** que casou com o padrão | `:%s/foo/[&]/` ou `:%s/foo/[\0]/` | Coloca colchetes ao redor de “foo” |
| `\v` | Very magic | Modo que simplifica a regex (sem precisar escapar tudo) | `:%s/\vfoo|bar/baz/` | Substitui “foo” **ou** “bar” por “baz” |
| `\s` | Espaço | Casa qualquer espaço, tab ou quebra de linha | `/\v\s+/` | Casa espaços múltiplos consecutivos |
| `\S` | Não-espaço | Casa qualquer coisa que **não** seja espaço | `/\v\S+/` | Casa uma palavra (sem espaços) |
| `\d` | Dígito | Casa números (`0–9`) | `/\v\d+/` | Casa “123” em “abc123def” |
| `\D` | Não-dígito | Casa tudo **que não seja número** | `/\v\D+/` | Casa “abc” em “abc123” |
| `\w` | Palavra | Casa letras, números e `_` | `/\v\w+/` | Casa identificadores (ex: nomes de variáveis) |
| `\W` | Não-palavra | Casa tudo **que não seja letra/número/_** | `/\v\W+/` | Casa espaços, pontuação etc. |
| `|` | OU lógico | Alterna entre padrões | `/\vfoo|bar/` | Casa “foo” ou “bar” |
| `{n,m}` | Intervalo de repetições | Controla quantas vezes o padrão se repete | `/\v\d{2,4}/` | Casa números de 2 a 4 dígitos |

---

## 🛠️ Exemplos práticos de substituição

| Comando | Explicação |
|----------|------------|
| `:%s/foo/bar/g` | Substitui todas as ocorrências de `foo` por `bar` |
| `:'<,'>s/^/# /` | Comenta as linhas selecionadas no modo visual |
| `:%s/\v +$//` | Remove espaços no final das linhas |
| `:%s/\v^([^,]+,[^,]+)$/\1,0,0/` | Adiciona `,0,0` em linhas CSV com só 2 colunas |
| `:%s/\v^(\d+)/[\1]/` | Coloca colchetes em torno de números no início da linha |
| `:%s/\vfoo(\d+)/bar\1/` | Substitui “foo123” por “bar123” (mantendo o número) |
| `:%s/\v(.*)/\U\1/` | Converte toda a linha pra maiúsculas |
| `:%s/\v(.*)/\L\1/` | Converte toda a linha pra minúsculas |

---

## ⚡ Dicas de uso no Neovim

| Ação | Atalho / Comando | Descrição |
|------|------------------|------------|
| Substituir globalmente | `:%s/padrao/substituto/g` | Em todo o arquivo |
| Substituir em linhas selecionadas | `:'<,'>s/padrao/substituto/` | Após selecionar no modo visual |
| Confirmar cada substituição | `:%s/padrao/substituto/gc` | Pergunta “y/n/a/q/l” a cada match |
| Pré-visualizar linhas afetadas | `:g/padrao/p` | Mostra apenas as linhas que casam |
| Desfazer substituição | `u` | Desfaz a última operação |
| Repetir última substituição | `:&` | Repete o último `:s` |
| Aplicar a mesma substituição a várias linhas | `:.,+3s/.../.../` | Aplica nas 4 próximas linhas |

---

## 💡 Exemplos de uso combinando regex + substituição

```vim
" Adicionar colunas faltantes em CSV
:%s/\v^([^,]+,[^,]+)$/\1,0,0/

" Comentar linhas selecionadas
:'<,'>s/^/# /

" Remover espaços extras no fim da linha
:%s/\v +$//

" Converter para maiúsculas
:%s/\v(.*)/\U\1/

### 💡 Observações

- Pressione `Esc` **só depois de digitar o que deseja** em `I`/`A`
- Em `Visual Block`, `i` e `a` (minúsculos) não têm efeito
