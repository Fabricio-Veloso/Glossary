# 🧠 Django: Estrutura Inicial do Projeto (`startproject`)

Após executar o comando:

```bash
django-admin startproject config .
```

O Django cria uma estrutura com os arquivos iniciais para configurar e controlar seu projeto. Esse documento explica cada um deles.

## 📁 Estrutura Inicial

```
.
├── manage.py
└── config/
    ├── __init__.py
    ├── asgi.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

## 🔧 Arquivos principais

### manage.py

- Um atalho para interagir com o Django via terminal.

- Você usará esse comando para rodar o servidor, aplicar migrações, criar apps etc.

_Exemplo_:

```
python manage.py runserver
python manage.py migrate
python manage.py startapp meu_app
```

### **init**.py

    Torna o diretório config/ um pacote Python válido.

    Pode estar vazio.

    Permite fazer imports do tipo from config import settings.

### asgi.py

    Define a interface ASGI (Assynchronous Server Gateway Interface).

    Necessário para suportar WebSockets, requisições assíncronas e servidores como Uvicorn ou Daphne.

    Exemplo de uso:

```
uvicorn config.asgi:application
```

### wsgi.py

    Interface WSGI (síncrona), usada por servidores tradicionais como Gunicorn ou mod_wsgi (Apache).

    A maioria dos deploys ainda usa essa versão se não houver necessidade de chamadas assíncronas.

### ⚙️ settings.py: Configurações do Projeto

#### Contém todas as configurações essenciais do Django. Vamos por partes:

BASE_DIR

    Representa o caminho raiz do projeto.

    Usado para construir caminhos relativos com segurança.

SECRET_KEY

    Chave usada para criptografia interna, como sessões e tokens CSRF.

    Mantenha em segredo absoluto em produção.

DEBUG

    Exibe erros detalhados durante o desenvolvimento.

    Nunca use True em produção.

ALLOWED_HOSTS

    Lista de domínios/IPs autorizados a acessar sua aplicação.

    Impede ataques do tipo Host Header Injection.

    Em produção, adicione seu domínio aqui:

    ALLOWED_HOSTS = ["meusite.com", "api.meusite.com"]

INSTALLED_APPS

    Lista de apps Django ativos no projeto.

    Inclui:

        Apps internos do Django (admin, auth, sessions)

        Apps de terceiros (ex: rest_framework)

        Apps que você criar (blog, usuarios, etc)

MIDDLEWARE = [
...
]

    Componentes que interceptam requisições/respostas.

    Usado para:

        Segurança

        Geração de sessões

        Prevenção de CSRF

        Compressão GZip

        Cabeçalhos HTTP adicionais

TEMPLATES  
Configura o sistema de templates (HTML dinâmico).

    DIRS: onde buscar arquivos .html fora dos apps.

    Exemplo: "DIRS": [BASE_DIR / "templates"]

DATABASES

    Define o banco de dados usado.

    Pode trocar ENGINE por:

        django.db.backends.postgresql

        django.db.backends.mysql

        django.db.backends.oracle

AUTH_PASSWORD_VALIDATORS = [...]

    Atuam em formulários de criação/alteração de senha.

LANGUAGE_CODE

    Define o idioma e o fuso horário padrão da aplicação.

USE_I18N

    Suporte à tradução

USE_L10N

    Formatação local de datas/números

USE_TZ

    Usa fuso horário (timezone-aware datetimes)

STATIC_URL, MEDIA_URL (não sempre visível no início)

    Usado para servir arquivos estáticos e de mídia (CSS, JS, imagens, uploads). Exemplo:

```
STATIC_URL = '/static/'
MEDIA_URL = '/media/'
```

DEFAULT_AUTO_FIELD

    Define o tipo de campo padrão para chaves primárias (id) nos models.

    BigAutoField é um inteiro de 64 bits (bom para crescimento de dados).

## ✅ Dica para Ambiente Local

Para evitar erros, crie seus projetos Django fora de diretórios do Windows (como /mnt/c). Prefira locais como:

```
~/projetos/brinc-django
```

## 🎯 Próximo passo sugerido

Crie seu primeiro app com:

```
python manage.py startapp meu_app
```

### _Depois, adicione ele no INSTALLED_APPS e comece a criar views, urls e models._

## 💡 Dica final

Use python manage.py help para ver todos os comandos disponíveis.
Ou python manage.py help <comando> para ajuda específica.
