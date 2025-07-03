# Glossário Prático para Relembrar Python

> Relembrar a linguagem após um tempo parado. Foco nas particularidades do Python comparado a outras linguagens.

---

## 🧠 Diferenças Notáveis (em relação a C, JavaScript, TypeScript, Java, etc.)

- **Indentação = Blocos**  
  Python usa indentação (espaços ou tabulação) para definir blocos de código — sem `{}` ou `begin/end`.

- **Sem ponto e vírgula**  
  Ao final das linhas, não é necessário `;`.

- **Variáveis dinamicamente tipadas**  
  Sem necessidade de declarar tipo (`int x = 10` → `x = 10`), mas pode usar type hints: `x: int = 10`.

- **Tudo é objeto**  
  Até tipos primitivos (int, str, list) têm métodos. Exemplo: `"abc".upper()`.

- **Ausência de switch/case**  
  Usa-se `if/elif/else` ou dicionários como alternativa.

- **Funções podem retornar múltiplos valores**  
  `return a, b` → tuple unpacking: `x, y = func()`.

---

## 🧾 Convenções e Sintaxe Rápida

### Declaração de funções

```
def minha_funcao(arg1, arg2=10) -> int:
    return arg1 + arg2
```

#### Tipagem opcional (Type Hints)

```
def soma(a: int, b: int) -> int:
    return a + b
```

#### Lista por compreensão (list comprehension)

```
 quadrados = [x**2 for x in range(10)]
```

#### F-strings (Interpolação moderna de strings)

```
nome = "Fab"
print(f"Olá, {nome}")
```

#### Dicionários e uso moderno

```
meu_dict = {"nome": "Fab", "idade": 30}
print(meu_dict.get("nome"))
```

### 🧪 Estruturas e Controle de Fluxo

#### for itera sobre qualquer iterável (sem i++)

```
for item in lista:
    print(item)

for i in range(5):  # range é gerador de números
    print(i)

while padrão

while condicao:
    # loop

try/except (sem catch)

try:
    # código
except ValueError:
    print("Erro de valor")
finally:
    print("Sempre executa")
```

### 🐍 Idiomaticamente Python (Pythonic Way)

    Evite for i in range(len(lista)) → use for item in lista

    Use unpacking: a, b = b, a

    Verifique listas vazias com if lista: em vez de len(lista) > 0

    Use enumerate e zip sempre que necessário

### 📦 Importações e Módulos

- import os
- from math import sqrt
- from meu_modulo import minha_funcao
- Evite import \*, prefira nomes explícitos.

### 📚 Padrões Comuns

with para contexto (ex: arquivos)

```
with open("arquivo.txt") as f:
    conteudo = f.read()
```

Funções lambda

```
soma = lambda x, y: x + y
```

Decoradores

```
def meu_decorador(func):
    def wrapper():
        print("Antes")
        func()
        print("Depois")
    return wrapper

@meu_decorador
def saudacao():
    print("Olá")
```

### 🔁 Iteráveis, Geradores e Iteradores

```
def gerador():
    for i in range(10):
        yield i  # Pausa e continua

for numero in gerador():
    print(numero)
```

### 🧩 Exclusivos ou Fortemente Associados ao Python

    Duck typing: “Se anda como um pato...”

    __init__, __str__, __repr__, etc.: Métodos mágicos

    List Comprehensions / Dict Comprehensions

    None como objeto nulo (não é null)

    is vs ==: is compara identidade, == compara valor

    pip e ambientes virtuais (venv/poetry/pipenv)

### 🔒 Extras (Boas práticas)

    Use venv para isolar dependências:

    python -m venv venv
    source venv/bin/activate  # Linux/mac
    .\venv\Scripts\activate   # Windows

    Organize por módulos: __init__.py define pacotes

    Use mypy ou pyright para checagem estática de tipos

### 📌 Cheatsheet Express

```
# String
s = "texto"
s.upper()

# Lista
lista = [1, 2, 3]
lista.append(4)

# Dicionário
d = {"a": 1}
d["b"] = 2

# Função com valor default
def f(x, y=2): return x + y

# Class
class Pessoa:
    def __init__(self, nome):
        self.nome = nome
```

---
