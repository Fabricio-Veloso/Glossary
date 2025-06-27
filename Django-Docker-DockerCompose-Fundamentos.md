# 🐳 Docker e Docker Compose – Fundamentos e Diagnóstico no Django

## 🎯 Objetivo

- Entender o papel de cada arquivo

  - Dockerfile
  - docker-compose.yml

- Como funciona o ciclo de vida dos containers e quais comandos são úteis para:

  - inspecionar
  - interagir
  - depurar

- ambientes Django em produção via Docker.

## 🧱 Diferença entre Dockerfile e docker-compose.yml

- **Dockerfile** Define:

  - A imagem base: ambiente, libs, dependências, código.

- **docker-compose.yml** Define:

  - Os serviços e como os containers devem ser orquestrados: volumes, portas, variáveis, etc.

### ✅ Você precisa dos dois: um define como construir o container, o outro define como executar o container no ecossistema do projeto.✅

## 🔁 Entendendo o fluxo padrão

    O Dockerfile cria a imagem personalizada

        Python + dependências + código do projeto

    O docker-compose usa essa imagem e define:

        Variáveis de ambiente

        Volumes (link com o código local)

        Portas expostas

        Comandos de inicialização (wait_for_db, migrate, runserver)

    Ao reiniciar o container, o Django roda automaticamente:

    python manage.py migrate

    Isso explica por que ao subir o container, as migrações são aplicadas automaticamente, mesmo que você não as execute manualmente.

🔍 Diagnóstico e Interação com o Container
✅ Ver containers em execução

docker ps

✅ Acessar o terminal bash dentro do container

docker exec -it nome_ou_id_do_container bash

Exemplo prático:

docker exec -it web bash

📁 Entendendo volumes e contexto de código

volumes:

- .:/app

  Isso mapeia o diretório do seu host (código local) para o diretório /app dentro do container.

⚠️ Isso significa:

    Alterações feitas fora do container aparecem imediatamente dentro dele

    Mas isso depende de o volume estar ativo

    Se você fizer docker-compose down --volumes, dados e links são perdidos

🧪 Conferir conteúdo do projeto dentro do container

docker exec -it web bash
cd /app
ls

🔥 Comandos úteis do dia a dia
Recompilar imagem e reiniciar containers (forçando rebuild)

docker-compose up --build

Apenas reiniciar containers (sem rebuild)

docker-compose up

Subir em segundo plano (modo daemon)

docker-compose up -d

Derrubar tudo

docker-compose down

Derrubar tudo e remover volumes (⚠️ apaga dados)

docker-compose down --volumes

🧠 Dicas finais

    Prefira ENTRYPOINT ou command: no docker-compose.yml para lógica de start dinâmica (como wait_for_db && migrate && runserver)

    Evite rodar makemigrations em produção. Esse comando deve ser feito localmente e versionado.

    Sempre verifique se os volumes estão ativos (docker volume ls) quando parecer que o código dentro do container está “desatualizado”.

    Cuide com os contextos diferentes: o que está na pasta local e o que está no container pode se desalinhar se não houver volume ativo.

    ✅ Este guia ajuda a manter clareza sobre o que está acontecendo no ambiente Docker e como navegar entre o código local e o container com confiança.
