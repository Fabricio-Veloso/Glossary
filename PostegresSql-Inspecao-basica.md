# 🧩 PostgreSQL – Inspeção e Diagnóstico Básico

## 🎯 Objetivo

Acessar um banco PostgreSQL e inspecionar estrutura sem retornar dados, ideal para entender o schema em uso (ex: tabelas existentes, colunas, relações).

---

### ✅ Acesso via terminal (psql)

```
psql -h localhost -U meu_usuario -d nome_do_banco
```

### 🔍 Listar todas as tabelas do schema atual

```
\dt
```

### Para incluir tabelas de todos os schemas:

```
\dt *.*
```

### 🧱 Ver estrutura de uma tabela (sem dados)

```
\d nome_da_tabela
```

### 📊 Ver quantos registros tem uma tabela

```
SELECT COUNT(*) FROM nome_da_tabela;
```

### 🧠 Identificar o modelo de usuário padrão do Django

    Se a tabela auth_user existir → modelo padrão em uso.

    Se houver outra tabela como meuapp_customuser → modelo customizado.

#### Para confirmar via Django:

```
from django.contrib.auth import get_user_model
print(get_user_model())
```

### 🧪 Ver os 5 primeiros registros de uma tabela

```
SELECT * FROM nome_da_tabela LIMIT 5;
```

### 💡 Extras úteis

#### Lista todos os bancos

```
\l
```

#### Conecta a outro banco

```
\c nome_do_banco

```

#### Mostra o schema atual

```
SHOW search_path;
```

#### Troca para o schema public

```
SET search_path TO public;
```

---
