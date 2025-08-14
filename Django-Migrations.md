# 🧱 Django – Migrações e Alterações em Modelos

## 📌 O que são migrações no Django?

Migrações são arquivos Python gerados pelo Django que descrevem as alterações no schema do banco de dados, com base em mudanças nos modelos (`models.py`).

---

## ✅ Fluxo padrão de alteração de modelos

1.  **Altere o modelo (ex: adicionar um atributo de e-mail em uma entidade de usuário `User`)**
2.  Gere as migrações:

    ```bash
    python manage.py makemigrations
    ```

    Aplique as migrações no banco:

        python manage.py migrate

### 🧠 Atenção especial em times

#### Situação Consequência

- Alterou o modelo mas não rodou makemigrations

  O banco não será atualizado

- Rodou makemigrations mas não comitou

  Outros devs não terão os arquivos .py

- Rodou makemigrations e migrate apenas localmente

  Produção permanece desatualizada

### ⚠️ Nunca rode makemigrations na produção se os arquivos já foram criados!⚠️

- Evite conflitos e redundâncias.
- Confirme antes se o diretório migrations/ já existe e está versionado.

### 📁 Estrutura típica após makemigrations

- meu_app/
  - migrations/
    - 0001_initial.py
    - **init**.py

### 🧪 Verificar o estado das migrações

```
python manage.py showmigrations
```

### 🛡️ Checklist seguro para ambientes com Docker

- Verificar se migrations/ existe no app
- Rodar apenas migrate no container de produção
- Evitar makemigrations em produção salvo se tiver certeza de que nada foi criado antes
- Sempre versionar e comitar as migrações geradas

### 🔄 Exemplo para aplicar em produção (dentro do container)

```
docker exec -it meu_container bash
cd /app
python manage.py migrate
```

### ✅ Use este guia ao lidar com alterações em modelos no Django, especialmente em ambientes versionados ou com múltiplos desenvolvedores.✅

---
