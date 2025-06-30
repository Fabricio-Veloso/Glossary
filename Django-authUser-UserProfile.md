# 🔐 Django – User padrão com extensão via UserProfile

## 🎯 Objetivo

- Compreender como o Django organiza os dados de usuários quando o modelo padrão auth_user é mantido, mas campos adicionais são adicionados via uma tabela auxiliar (UserProfile), e como inspecionar isso corretamente no banco de dados PostgreSQL.
  ✅ Estrutura usada

- O projeto usa o modelo padrão do Django (auth_user) para autenticação, enquanto campos extras como cpf, rnp, etc., são armazenados em uma tabela separada (ex: eventos_userprofile), relacionada 1:1.
  🔗 Modelo típico no Django

```
from django.contrib.auth.models import User
from django.db import models
```

```
class UserProfile(models.Model):

user = models.OneToOneField(User, on_delete=models.CASCADE)

cpf = models.CharField(max_length=14)

rnp = models.CharField(max_length=20)
```

## 📁 Admin com dados estendidos

```
from django.contrib import admin
from .models import UserProfile
```

```
@admin.register(UserProfile)

class UserProfileAdmin(admin.ModelAdmin):

list_display = ('user', 'cpf', 'rnp')
```

## 📊 Visualização no banco (PostgreSQL)

### Ver estrutura da tabela auth_user

```
\d auth_user
```

- Campos padrão: username, email, password, etc.
- Campos adicionais como cpf, rnp não aparecem aqui, pois estão em outro lugar.
- Ver estrutura da tabela estendida

```
\d eventos_userprofile
```

### Aqui devem aparecer os campos cpf, rnp, e uma chave estrangeira user_id para auth_user.id.

#### 🧪 Consultar dados combinando as duas tabelas

```
SELECT eup.cpf, eup.rnp, au.username
FROM eventos_userprofile eup
JOIN auth_user au ON eup.user_id = au.id;
```

- Essa query mostra os dados de autenticação junto com os dados adicionais.

### 🔍 Ver um registro completo de forma legível

Modo expandido (psql)

```
\x
```

#### Ver o perfil de um usuário

```
SELECT \* FROM eventos_userprofile WHERE user_id = 1;
```

#### Voltar ao modo normal:

```
\x
```

#### 🧠 Confirme no código se o modelo padrão está em uso

- Se não houver isso no settings.py:

```
AUTH_USER_MODEL = 'app.CustomUser'
```

- Então o Django está usando auth_user.

### 💡 Por que essa abordagem é usada?

- 🔧 Simples de implementar Não exige alterar settings.py ou migrar apps
- 🧱 Evita conflito com pacotes Mantém compatibilidade com apps que dependem de auth_user
- 🪛 Modularidade Permite separação de responsabilidades entre autenticação e dados do usuário
