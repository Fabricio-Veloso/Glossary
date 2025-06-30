# Arquitetura Onion Adaptada para Projetos Django 🍥📦📐

## Parte 1: Conceito Geral da Onion Architecture (Independente de Framework) 🧠🧭📚

### Objetivo 🎯📌🛠️

Organizar o sistema em camadas concêntricas para separar bem as responsabilidades e evitar acoplamento entre as partes. O centro da aplicação contém a lógica de negócio e as bordas cuidam da comunicação com o mundo externo (HTTP, banco de dados, APIs etc). 🎯📌🛠️

### Camadas Principais 🪆🧩🏗️

#### 1. **Domain (Domínio)** 🧱🔐🧬

- Representa os conceitos do mundo real do sistema (ex: Aluno, Produto, Pedido).
- Contém as **regras de negócio puras**, sem dependências de frameworks ou tecnologias externas.
- Exemplo: validar email, calcular preço com desconto, verificar CPF, etc.

#### 2. **Application (Aplicação / Casos de Uso)** 🛠️⚙️🎯

- Coordena os processos da aplicação.
- Recebe dados, instancia entidades do domínio, chama métodos, usa repositórios.
- Aqui ficam os "serviços" como: CriarAluno, EfetuarPagamento, GerarRelatório.

#### 3. **Infrastructure (Infraestrutura / Detalhes Técnicos)** 🧰🔌🗄️

- Implementa as dependências externas: banco de dados, APIs externas, email, etc.
- Usa ferramentas específicas (ORM, bibliotecas, integrações, etc).

#### 4. **Interfaces (Interface com o exterior)** 🌐📨🔁

- Controladores, endpoints HTTP, consumers WebSocket, formulários HTML, etc.
- É a porta de entrada para o sistema.

### Fluxo de Dados 🔄📥📤

```
Usuário (front-end ou outro sistema)
    ↓
Interface (views, API, formulário)
    ↓
Application (serviços / casos de uso)
    ↓
Domain (entidades, validações)
    ↓
Infrastructure (banco de dados, envio de email)
    ↑
Retorno (status, resultado, erro)
```

---

## Parte 2: Implementando a Onion Architecture com Django 🐍🏗️🧱

### Premissas 📋⚠️🔧

- Django não impõe uma arquitetura, mas pode ser adaptado para suportar essa estrutura.
- É recomendado criar subpastas manuais dentro do seu app para organizar as camadas. 📋⚠️🔧

### Estrutura Recomendada 🗂️📁🔨

```
estudandopython/
├── domain/            # Entidades e regras de negócio
│   └── aluno.py
├── application/       # Serviços e casos de uso
│   └── cadastrar_aluno.py
├── infrastructure/    # Repositórios, ORM, integrações
│   └── aluno_repository.py
├── interfaces/        # Views, endpoints, serializers, etc
│   └── aluno_view.py
├── models.py          # Pode conter models do Django para uso interno
├── urls.py            # Roteamento
└── ... (outros arquivos padrão do app Django)
```

### Exemplo Prático 💡👨‍💻🔍

#### `domain/aluno.py`

```python
class Aluno:
    def __init__(self, nome, email):
        self.nome = nome
        self.email = email

    def validar_email(self):
        if "@" not in self.email:
            raise ValueError("Email inválido")
```

#### `application/cadastrar_aluno.py`

```python
from domain.aluno import Aluno

class CadastrarAluno:
    def __init__(self, repositorio):
        self.repositorio = repositorio

    def executar(self, nome, email):
        aluno = Aluno(nome, email)
        aluno.validar_email()
        self.repositorio.salvar(aluno)
```

#### `infrastructure/aluno_repository.py`

```python
from estudandopython.models import AlunoModel

class AlunoRepositoryDjango:
    def salvar(self, aluno):
        AlunoModel.objects.create(nome=aluno.nome, email=aluno.email)
```

#### `interfaces/aluno_view.py`

```python
from django.http import JsonResponse
from application.cadastrar_aluno import CadastrarAluno
from infrastructure.aluno_repository import AlunoRepositoryDjango

def cadastrar_aluno_view(request):
    nome = request.POST.get('nome')
    email = request.POST.get('email')

    caso_de_uso = CadastrarAluno(AlunoRepositoryDjango())
    try:
        caso_de_uso.executar(nome, email)
        return JsonResponse({'mensagem': 'Aluno cadastrado com sucesso'})
    except Exception as e:
        return JsonResponse({'erro': str(e)}, status=400)
```

### Model para o Django (em `models.py`) 🗃️📄📌

```python
from django.db import models

class AlunoModel(models.Model):
    nome = models.CharField(max_length=100)
    email = models.EmailField(unique=True)
```

### `urls.py` 🌍🛣️📥

```python
from django.urls import path
from interfaces.aluno_view import cadastrar_aluno_view

urlpatterns = [
    path('api/alunos/', cadastrar_aluno_view),
]
```

---

## Conclusão ✅🧩🚀

- Essa estrutura dá mais clareza, escalabilidade e testabilidade.
- Ela separa responsabilidades: cada camada tem um papel claro.
- Apesar de mais "manual", ela se aproxima das boas práticas de arquiteturas modernas. ✅🧩🚀

Se quiser evoluir para usar Django REST Framework ou FastAPI no lugar das interfaces, ou SQLAlchemy na infraestrutura, essa separação ajuda muito na manutenção e flexibilidade do sistema. ✅🧩🚀
