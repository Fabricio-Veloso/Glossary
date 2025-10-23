# 🐍 Setup e Boas Práticas com Python + Django

Este documento descreve como configurar rapidamente o ambiente de desenvolvimento Python/Django, tanto no **Windows (PowerShell)** quanto no **WSL/Linux**, com foco em boas práticas e reprodutibilidade.

---

## 🪟 Setup no Windows

### 📦 Instalações iniciais

1. **Baixar e instalar o Python (>=3.10)**  
   👉 [https://www.python.org/downloads/](https://www.python.org/downloads/)  
   Durante a instalação:
   - Marque **“Add Python to PATH”**
   - Marque **“Install for all users”**

2. **Verificar instalação**
   ```powershell
   python --version
   pip --version

    (Opcional) Instalar o Git

e confirmar:

    git --version

🧱 Criando um novo projeto Django com venv

# Criar diretório do projeto
mkdir nome_do_projeto
cd nome_do_projeto

# Criar ambiente virtual
python -m venv venv

# Ativar ambiente virtual
.\venv\Scripts\activate

# Atualizar pip
python -m pip install --upgrade pip

# Instalar Django
pip install django

# Criar projeto
django-admin startproject config .

# Rodar servidor local
python manage.py runserver

🔁 Checklist para projeto existente

# Entrar no projeto
cd nome_do_projeto

# Criar e ativar o ambiente virtual
python -m venv venv
.\venv\Scripts\activate

# Instalar dependências
pip install -r requirements.txt

# Aplicar migrações
python manage.py migrate

# Rodar servidor
python manage.py runserver

⚙️ Boas práticas (Windows)

    Sempre usar ambientes virtuais (venv, pipenv ou poetry)

    Evitar instalar pacotes com pip install fora do venv

    Versionar o arquivo requirements.txt

    Evitar usar sudo ou privilégios de admin desnecessariamente

    Se activate for bloqueado, liberar scripts:

Set-ExecutionPolicy RemoteSigned -Scope CurrentUser

Desativar o ambiente:

    deactivate

🛠 Ferramentas úteis

pip install black flake8 ipython django-debug-toolbar

💡 Dica: Configure o Neovim para usar PowerShell como terminal:

if vim.loop.os_uname().sysname == "Windows_NT" then
  vim.o.shell = "pwsh"
  vim.o.shellcmdflag = "-NoLogo -NoProfile -ExecutionPolicy RemoteSigned -Command"
  vim.o.shellquote = ""
  vim.o.shellxquote = ""
end

🐧 Setup no WSL / Linux
📦 Instalações iniciais

sudo apt update
sudo apt install python3 python3-pip python3-venv pipx -y

✅ Configurar PATH (se necessário):

echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

⚙️ Instalar ferramentas com pipx

pipx install pipenv
pipx install black
pipx install httpie

🧱 Criar novo projeto Django com Pipenv

mkdir nome_do_projeto
cd nome_do_projeto

# Criar ambiente virtual e instalar Django
pipenv install django

# Ativar o ambiente
pipenv shell

# Criar o projeto
django-admin startproject config .

# Rodar servidor
python manage.py runserver

🔁 Projeto existente

cd nome_do_projeto

# Instalar dependências
pipenv install

# Ativar ambiente virtual
pipenv shell

# Aplicar migrações
python manage.py migrate

# Rodar servidor
python manage.py runserver

🎯 Boas práticas (WSL/Linux)

    Sempre usar pipenv, venv ou poetry para isolar dependências

    Evitar sudo pip install (risco de corromper o Python do sistema)

    Versionar Pipfile e Pipfile.lock

    Usar pipx apenas para ferramentas globais

    Para deletar um ambiente corrompido:

    pipenv --rm

🛠 Comandos úteis

exit                     # Sair do ambiente virtual
pipenv graph             # Ver dependências
pipenv update            # Atualizar pacotes
pipenv install nome_lib  # Instalar nova dependência
pipenv uninstall nome_lib
pipenv --rm              # Remover ambiente virtual

🔄 Migração de WSL para Windows

Se você já tinha um projeto no WSL e quer continuar no Windows, siga estes passos:
1. Copiar o projeto

No Windows, crie uma pasta onde o projeto será colocado, e copie apenas os arquivos de código, não o ambiente virtual:

    Copie tudo exceto:

        .venv/ ou venv/

        __pycache__/

        .mypy_cache/

2. Criar novo ambiente virtual no Windows

cd C:\caminho\para\seu\projeto
python -m venv venv
.\venv\Scripts\activate

3. Reinstalar dependências

Se o projeto usava pipenv:

pip install pipenv
pipenv install

Se usava requirements.txt:

pip install -r requirements.txt

4. Ajustar caminhos em configurações

    Se o seu settings.py tinha caminhos absolutos (/home/...), substitua por caminhos relativos usando BASE_DIR / 'subpasta'.

    Verifique permissões e PATH de banco de dados (ex: SQLite) se o arquivo .db estava dentro do WSL.

5. Testar o servidor

python manage.py runserver

Se tudo rodar sem erro, o ambiente está pronto ✅
📚 Referências

    Documentação do Pipenv

Documentação do pipx

Django Getting Started


---

Quer que eu adicione no final uma mini seção de **“Resolução de problemas comuns”** (como erros de `activate`, conflitos de `pipenv`, e falhas de migração SQLite)? Isso deixaria o glossário à prova de sustos.

You said:
Coloca tudo em um documento só, por favor
ChatGPT said:

Perfeito, Fab 👍
Aqui está o documento completo — unificado, formatado em Markdown puro, com as seções para Windows, WSL/Linux e Migração entre ambientes.
Pronto pra copiar e colar direto no seu arquivo ambientes-python-wsl.md:

# 🐍 Setup e Boas Práticas com Python + Django

Este documento descreve como configurar rapidamente o ambiente de desenvolvimento Python/Django, tanto no **Windows (PowerShell)** quanto no **WSL/Linux**, com foco em boas práticas, reprodutibilidade e migração entre ambientes.

---

## 🪟 Setup no Windows

### 📦 Instalações iniciais

1. **Baixar e instalar o Python (>=3.10)**  
   👉 [https://www.python.org/downloads/](https://www.python.org/downloads/)  
   Durante a instalação:
   - Marque **“Add Python to PATH”**
   - Marque **“Install for all users”**

2. **Verificar instalação**
   ```powershell
   python --version
   pip --version

    (Opcional) Instalar o Git

e confirmar:

    git --version

🧱 Criando um novo projeto Django com venv

# Criar diretório do projeto
mkdir nome_do_projeto
cd nome_do_projeto

# Criar ambiente virtual
python -m venv venv

# Ativar ambiente virtual
.\venv\Scripts\activate

# Atualizar pip
python -m pip install --upgrade pip

# Instalar Django
pip install django

# Criar projeto
django-admin startproject config .

# Rodar servidor local
python manage.py runserver

🔁 Checklist para projeto existente

# Entrar no projeto
cd nome_do_projeto

# Criar e ativar o ambiente virtual
python -m venv venv
.\venv\Scripts\activate

# Instalar dependências
pip install -r requirements.txt

# Aplicar migrações
python manage.py migrate

# Rodar servidor
python manage.py runserver

⚙️ Boas práticas (Windows)

    Sempre usar ambientes virtuais (venv, pipenv ou poetry)

    Evitar instalar pacotes com pip install fora do venv

    Versionar o arquivo requirements.txt

    Evitar usar sudo ou privilégios de admin desnecessariamente

    Se activate for bloqueado, liberar scripts:

Set-ExecutionPolicy RemoteSigned -Scope CurrentUser

Desativar o ambiente:

    deactivate

🛠 Ferramentas úteis

pip install black flake8 ipython django-debug-toolbar

💡 Dica: Configure o Neovim para usar PowerShell como terminal:

if vim.loop.os_uname().sysname == "Windows_NT" then
  vim.o.shell = "pwsh"
  vim.o.shellcmdflag = "-NoLogo -NoProfile -ExecutionPolicy RemoteSigned -Command"
  vim.o.shellquote = ""
  vim.o.shellxquote = ""
end

🐧 Setup no WSL / Linux
📦 Instalações iniciais

sudo apt update
sudo apt install python3 python3-pip python3-venv pipx -y

✅ Configurar PATH (se necessário):

echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

⚙️ Instalar ferramentas com pipx

pipx install pipenv
pipx install black
pipx install httpie

🧱 Criar novo projeto Django com Pipenv

mkdir nome_do_projeto
cd nome_do_projeto

# Criar ambiente virtual e instalar Django
pipenv install django

# Ativar o ambiente
pipenv shell

# Criar o projeto
django-admin startproject config .

# Rodar servidor
python manage.py runserver

🔁 Projeto existente

cd nome_do_projeto

# Instalar dependências
pipenv install

# Ativar ambiente virtual
pipenv shell

# Aplicar migrações
python manage.py migrate

# Rodar servidor
python manage.py runserver

🎯 Boas práticas (WSL/Linux)

    Sempre usar pipenv, venv ou poetry para isolar dependências

    Evitar sudo pip install (risco de corromper o Python do sistema)

    Versionar Pipfile e Pipfile.lock

    Usar pipx apenas para ferramentas globais

    Para deletar um ambiente corrompido:

    pipenv --rm

🛠 Comandos úteis

exit                     # Sair do ambiente virtual
pipenv graph             # Ver dependências
pipenv update            # Atualizar pacotes
pipenv install nome_lib  # Instalar nova dependência
pipenv uninstall nome_lib
pipenv --rm              # Remover ambiente virtual

🔄 Migração de WSL para Windows

Se você já tinha um projeto no WSL e quer continuar no Windows, siga estes passos:
1. Copiar o projeto

No Windows, crie uma pasta onde o projeto será colocado, e copie apenas os arquivos de código, não o ambiente virtual:

    Copie tudo exceto:

        .venv/ ou venv/

        __pycache__/

        .mypy_cache/

2. Criar novo ambiente virtual no Windows

cd C:\caminho\para\seu\projeto
python -m venv venv
.\venv\Scripts\activate

3. Reinstalar dependências

Se o projeto usava pipenv:

pip install pipenv
pipenv install

Se usava requirements.txt:

pip install -r requirements.txt

4. Ajustar caminhos em configurações

    Se o seu settings.py tinha caminhos absolutos (/home/...), substitua por caminhos relativos usando BASE_DIR / 'subpasta'.

    Verifique permissões e PATH de banco de dados (ex: SQLite) se o arquivo .db estava dentro do WSL.

5. Testar o servidor

python manage.py runserver

Se tudo rodar sem erro, o ambiente está pronto ✅
🧩 Resolução de Problemas Comuns
⚠️ Erro ao ativar venv no Windows

.\venv\Scripts\activate : File cannot be loaded because running scripts is disabled on this system.

✅ Solução:

Set-ExecutionPolicy RemoteSigned -Scope CurrentUser

🧱 Erro “ModuleNotFoundError: No module named 'venv'”

Seu Python foi instalado sem o módulo venv.
Reinstale o Python e marque a opção “Virtual Environment” no instalador.
🧰 Problemas ao migrar SQLite

Se o banco de dados .db foi criado no WSL, recrie as migrações no Windows:

python manage.py migrate --fake
python manage.py makemigrations
python manage.py migrate

🧩 “pipenv not found”

Reinstale via pipx ou pip:

pip install pipenv
