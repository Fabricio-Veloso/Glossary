## ✅ 1. O que o root faz no Nginx?

A diretiva root define o caminho no sistema de arquivos onde os arquivos estáticos estão localizados. Ou seja, ela aponta para uma pasta no disco (e não tem nada a ver com o root do sistema operacional tipo / ou o "usuário root").

No seu exemplo:

```
server {
    listen 8080;
    root /data/up1;

    location / {
    }
}
```

A linha root /data/up1; está dizendo:

    “Para as requisições que forem tratadas por esse bloco location, e que não tenham um root específico dentro do location, os arquivos vão ser buscados na pasta /data/up1 no disco.”

## ✅ 2. O root está se referindo à rota /?

Não exatamente.

    O root não se refere à rota / da URL.

    Ele se refere ao caminho de arquivos no disco.

    A rota / no location / {} é o caminho da URL, ou seja, “quando alguém acessa http://localhost:8080/”.

O Nginx vai combinar isso com o root para encontrar os arquivos no disco.

## 🔄 O root pode ser sobrescrito por um location?

Sim. Se você colocar um root dentro do location, ele sobrescreve o root do nível server.

Exemplo:

```
server {
    listen 8080;
    root /data/up1;

    location /img/ {
        root /mnt/assets;
    }
}
```

Se você acessar /img/logo.png, o Nginx vai procurar:

/mnt/assets/img/logo.png

(E não /mnt/assets/logo.png, porque ele junta o root com o path completo da URL.)

Se quiser que ele não repita /img/ ao juntar, você usaria alias em vez de root — mas esse é outro papo.

## 🧑‍💻 1. Para que serve a diretiva user no Nginx?

user nobody;

📌 Função:

Define qual usuário do sistema operacional o processo worker do Nginx vai usar após a inicialização.

    O processo master (geralmente iniciado como root) precisa de privilégios elevados para, por exemplo, abrir portas < 1024.

    Depois que o master inicia os workers, eles podem operar com permissões mais restritas por segurança. É aí que entra a diretiva user.

🔐 Exemplo prático:

user www-data;

    Muito comum em distros Linux com Nginx instalado por package manager.

    Os arquivos que o Nginx vai servir (como /var/www/html) precisam estar acessíveis por esse usuário (www-data, no exemplo).

🔍 E se você deixar sem user?

    O padrão costuma ser nobody ou nginx, dependendo da distro.

    Se o Nginx foi iniciado como root e não tiver user configurado, os workers continuarão como root, o que não é seguro.

## 2. Estrutura de arquivos de configuração no Nginx

O Nginx lê apenas um arquivo principal, por padrão:

```
/etc/nginx/nginx.conf
```

Mas esse arquivo pode incluir outros arquivos, usando a diretiva include.
✅ Boas práticas:

- Colocar configurações de servidores individuais ou blocos em arquivos separados, dentro de:

```
/etc/nginx/conf.d/

OU

/etc/nginx/sites-available/ (usado com symlink para sites-enabled/)
```

### 🧠 Exemplo típico:

No nginx.conf:

```
http {
    include /etc/nginx/mime.types;
    include /etc/nginx/conf.d/*.conf;
}

Cada arquivo .conf em conf.d/ pode conter:

server {
    listen 80;
    server_name exemplo.com;
    root /var/www/exemplo;
}
```

Assim, você pode modularizar seu setup. Exemplo:

    default.conf → site principal

    api.conf → backend API

    admin.conf → painel de admin

    ssl.conf → configuração compartilhada de TLS

### 🚀 3. Usando arquivos diferentes de configuração

Você pode rodar o Nginx com qualquer arquivo de configuração custom, sem tocar no /etc/nginx/nginx.conf.
👇 Comando:

```
nginx -c /caminho/personalizado/meu_nginx.conf
```

Isso é útil, por exemplo:

- Em testes locais

- Em ambientes de CI/CD

- Em containers

## 🔄 Reload vs Start vs Test

    nginx -s reload
    👉 Recarrega a configuração sem parar o servidor (ideal para aplicar mudanças).

    nginx -s stop
    👉 Encerra o Nginx.

    nginx -t
    👉 Testa a sintaxe da configuração, sem aplicar. Muito importante antes de um reload:

    nginx -t -c /caminho/personalizado/meu_nginx.conf

## 💡 Dicas práticas

- Nunca edite diretamente o nginx.conf em produção.
- Use includes e versionamento.
- Separe responsabilidades:
- Um arquivo para logs
- Um para gzip/cache
- Um para balanceamento
- Um por app/site
- Permissões dos arquivos são críticas.
- O user configurado precisa conseguir ler os arquivos e pastas definidos no root.
- Considere usar symlinks com sites-available e sites-enabled, como o Apache faz.
- Isso facilita habilitar/desabilitar configs com:
  - ln -s /etc/nginx/sites-available/meusite.conf /etc/nginx/sites-enabled/

## 🧠 Outras variáveis úteis:

#### Variável O que representa

```
$uri         	   Caminho da URL normalizado (sem args, etc.)
$request_uri       Caminho da URL completo com query string
$host	           Host da requisição (api.seudominio.com)
$remote_addr       IP do cliente
$http_user_agent   User-Agent do navegador
$args Query string (param1=foo&param2=bar)
```

## Diretivas úteis:

### 🔹 proxy_pass

Encaminha a requisição para um destino.
Aceita:

- HTTP (backend web)
- HTTPS (backend seguro)
- Endereço IP ou domínio
- Com ou sem caminho

Exemplos:

```
proxy_pass http://localhost:5000;
proxy_pass https://api.seuservidor.com;
```

- 🧠 Dica avançada: Se você usa location /api/, e faz proxy_pass http://localhost:5000/, o sufixo / afeta como a URL é reescrita. Isso pode quebrar rotas se mal usado.

### 🔹 proxy_http_version

Usado quando o backend exige uma versão específica do HTTP.

    1.1: padrão moderno

    1.0: raramente necessário hoje

    2: não é suportado por proxy_pass (Nginx não faz proxy com HTTP/2 upstream, apenas downstream)

    ⚠️ Use 1.1 especialmente se o backend usar WebSockets.

### 🔹 proxy_set_header

Permite alterar ou definir headers que serão enviados ao backend.
Exemplos importantes:

```
proxy_set_header Host $host; # Domínio original (ex: meusite.com)
proxy_set_header X-Real-IP $remote_addr; # IP real do cliente
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for; # Lista de IPs
proxy_set_header X-Forwarded-Proto $scheme; # http ou https
```

Esses headers são úteis porque o backend, por padrão, não sabe:

- Qual era o IP do cliente
- Se a requisição veio de HTTPS
- Qual domínio foi acessado
- ASP.NET Core, por exemplo, pode se basear nesses headers para redirecionamentos, geração de links, autenticação, etc.

### 🔹 proxy_cache_bypass

- Controla quando o Nginx deve ignorar o cache (se estiver configurado).

```
proxy_cache_bypass $http_upgrade;
```

- Significa: "se o header Upgrade estiver presente, não use o cache".
- Isso é importante para WebSockets, SSE, etc., que não podem ser cacheados.

### 🔹 proxy_redirect

- Controla se o Nginx deve reescrever cabeçalhos Location vindos do backend.

```
proxy_redirect off;

Ou:

proxy_redirect http://localhost:5000/ https://meusite.com/;
```

- Útil quando o backend gera URLs absolutas para redirecionamento.

### 🔹 proxy_read_timeout, proxy_connect_timeout, proxy_send_timeout

Define timeouts da comunicação com o backend.

```
proxy_connect_timeout 10s;
proxy_send_timeout 30s;
proxy_read_timeout 30s;
```

- Esses valores evitam travamento caso o backend esteja lento ou não responda.

### 🔹 proxy_buffering

Habilita ou desabilita buffer entre Nginx e backend. Por padrão, é on.

proxy_buffering off;

- Útil se você quer streaming de dados em tempo real (ex: logs, SSE).

## 🍽️ Montando seu próprio "prato"

Você pode montar o bloco location /api/ como quiser, dependendo das suas necessidades. Aqui vai um exemplo mais completo:

location /api/ {
proxy_pass http://localhost:5000;

```
# Segurança e contexto do cliente
proxy_set_header Host $host;
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_set_header X-Forwarded-Proto $scheme;

# Suporte a WebSockets (opcional)
proxy_http_version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection "upgrade";

# Controle de cache e tempo de resposta
proxy_cache_bypass $http_upgrade;
proxy_connect_timeout 10s;
proxy_read_timeout 30s;
proxy_send_timeout 30s;

# Reescrita de redirecionamento se o backend gera URLs absolutas
proxy_redirect off;

}
```

## Opções importantes

### Server Slow-Start

- The server slow‑start feature prevents a recently recovered server from being overwhelmed by connections, which may time out and cause the server to be marked as failed again.

- In NGINX Plus, slow‑start allows an upstream server to gradually recover its weight from 0 to its nominal value after it has been recovered or became available. This can be done with the slow_start parameter to the server directive:

```
upstream backend {
    server backend1.example.com slow_start=30s;
    server backend2.example.com;
    server 192.0.0.1 backup;
}
```

- The time value (here, 30 seconds) sets the time during which NGINX Plus ramps up the number of connections to the server to the full value.

- Note that if there is only a single server in a group, the max_fails, fail_timeout, and slow_start parameters to the server directive are ignored and the server is never considered unavailable.

### ✅ HTTP Health Checks

📌 O que são?

São verificações automáticas feitas pelo balanceador de carga (como o Nginx) para saber se um servidor backend (ex: sua API ASP.NET) está saudável e pode receber requisições.

    Isso evita que o Nginx envie requisições para servidores que estão offline, lentos ou com erro.

🧪 Como funciona:

    O Nginx faz requisições periódicas (ex: GET /health) para o backend.

    Se o backend responde com um código 200 OK, ele é considerado saudável.

    Se responde com erro (ex: 500, 502) ou não responde, o Nginx pode tirá-lo temporariamente do pool.
