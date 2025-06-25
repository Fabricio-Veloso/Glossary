ambientes-python-wsl.md

# 🐍 Setup e Boas Práticas com Python + Django no WSL

## 📦 Instalações iniciais no WSL

```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv pipx

✅ Configurar PATH (se necessário)

echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

⚙️ Usando pipx para instalar ferramentas

pipx install pipenv

Outras úteis:

pipx install black
pipx install httpie

🧱 Criando um novo projeto Django com Pipenv

mkdir nome_do_projeto
cd nome_do_projeto

# Criar ambiente virtual com pipenv e instalar Django
pipenv install django

# Ativar o ambiente
pipenv shell

# Criar o projeto
django-admin startproject config .

# Rodar o servidor
python manage.py runserver

🔁 Checklist ao iniciar um projeto Python/Django existente

cd nome_do_projeto

# Instalar dependências do projeto
pipenv install

# Ativar o ambiente virtual
pipenv shell

# Aplicar migrações
python manage.py migrate

# Rodar o servidor
python manage.py runserver

🎯 Boas práticas

    Sempre usar ambientes virtuais (pipenv, venv, ou poetry);

    Nunca instalar pacotes diretamente com pip install fora do venv;

    Usar pipenv install para adicionar libs e manter o Pipfile.lock;

    Sempre comitar o Pipfile e Pipfile.lock para manter a compatibilidade no time;

    Evitar sudo pip install — risco de quebrar o Python do sistema;

    Usar pipx para ferramentas globais e de linha de comando;

    Para deletar um venv corrompido: pipenv --rm.

🛠 Comandos úteis

# Sair do ambiente virtual
exit

# Ver dependências do projeto
pipenv graph

# Atualizar pacotes
pipenv update

# Instalar nova dependência
pipenv install nome_do_pacote

# Remover dependência
pipenv uninstall nome_do_pacote

# Remover ambiente virtual
pipenv --rm

📚 Referências

    Documentação oficial do Pipenv

    Documentação do pipx

    Django Getting Started


---

Se quiser, posso transformar esse `.md` em um arquivo real que você possa baixar aqui mesmo. Deseja que eu gere o arquivo?


```
