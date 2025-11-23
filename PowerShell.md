# 📘 Glossário PowerShell – Automação Pessoal, Scripts e Boas Práticas

## 🔹 1. Variáveis e Caminhos

### $PSScriptRoot
- Contém o caminho do diretório onde o script atual está sendo executado.  
Usar isso evita hardcode de caminhos absolutos e garante portabilidade.

```powershell
$basePath = "$PSScriptRoot\scripts\ps1Scripts"
Write-Host "Base: $basePath"
```
### Variáveis de ambiente

- Acessadas com $env:, permitem obter informações do sistema.

```powershell
Write-Host "Usuário atual: $env:USERNAME"
Write-Host "Pasta do usuário: $env:USERPROFILE"
```
- 💡 Dica: Sempre que possível, use $PSScriptRoot e $env: para tornar scripts independentes do computador.
---
### 🔹 2. Importação de Scripts e Funções

- Para evitar múltiplas instruções de import, use Get-ChildItem + ForEach-Object para importar recursivamente todos os .ps1:
```powershell
$basePath = "$PSScriptRoot\scripts\ps1Scripts"
Get-ChildItem -Path $basePath -Filter *.ps1 -Recurse | ForEach-Object {
    . $_.FullName
}
```
- O ponto (.) é o dot-sourcing: ele carrega o conteúdo do script no escopo atual (funções, variáveis, etc).
---
### 🔹 3. Funções

- Definem blocos reutilizáveis de lógica. Sempre prefira funções em vez de scripts longos.
```powershell
function Greet {
    param($name)
    Write-Host "Olá, $name!"
}

Greet -name "Fab"
```
- 💡 Use param() para facilitar a passagem de argumentos e tornar a função mais genérica.
---
### 🔹 4. Controle de Fluxo
- if / else
```powershell
$hour = (Get-Date).Hour
if ($hour -lt 12) {
    Write-Host "Bom dia!"
} else {
    Write-Host "Boa tarde!"
}
```
- switch
```powershell
$option = "B"
switch ($option) {
    "A" { Write-Host "Escolheu A" }
    "B" { Write-Host "Escolheu B" }
    Default { Write-Host "Opção inválida" }
}
```

- Loops (for, foreach, while)
```powershell
foreach ($n in 1..5) {
    Write-Host "Número: $n"
}
```
---
### 🔹 5. Manipulação de Arquivos e Diretórios
- Listar arquivos
```powershell
Get-ChildItem -Path "$PSScriptRoot\logs" -Filter *.log
```
- Criar pasta se não existir
```powershell
$dir = "$PSScriptRoot\data"
if (-not (Test-Path $dir)) {
    New-Item -ItemType Directory -Path $dir
}
```
- Copiar, mover e remover arquivos
```powershell
Copy-Item -Path "C:\temp\file.txt" -Destination "C:\backup\file.txt"
Move-Item -Path "C:\temp\file.txt" -Destination "C:\backup\"
Remove-Item -Path "C:\temp\old.txt" -WhatIf
```
- 💡 -WhatIf mostra o que aconteceria sem executar — excelente prática para evitar erros.
---
### 🔹 6. Pipelines e Objetos

 - PowerShell trabalha com objetos, não apenas texto. Isso torna o pipeline poderoso.

```powershell
Get-Process | Where-Object {$_.CPU -gt 100} | Sort-Object CPU -Descending
```
- 💡 Cada comando envia objetos para o próximo — use $_ para acessar propriedades.
---
### 🔹 7. Splatting (Passagem de Parâmetros Avançada)

- Permite passar vários parâmetros de forma legível:

```powershell
$params = @{
    Path = "C:\temp\file.txt"
    Destination = "D:\backup\file.txt"
    Force = $true
}
Copy-Item @params
```
---
### 🔹 8. Tratamento de Erros (Try / Catch / Finally)
```powershell
try {
    Copy-Item -Path "C:\temp\nofile.txt" -Destination "D:\backup"
} catch {
    Write-Host "Erro: $_"
} finally {
    Write-Host "Finalizado."
}
```
- 💡 Sempre use try/catch ao manipular arquivos, rede ou entrada do usuário.
---
### 🔹 9. Variáveis Automáticas Úteis
```powershell
Variável	Descrição
$?         	True se o último comando teve sucesso
$LASTEXITCODE	Código de saída do último comando externo
$_	        Objeto atual em loops/pipelines
$args	       Argumentos passados para o script/função

ping google.com
if ($?) { Write-Host "Conexão ok!" }
```
---
### 🔹 10. Boas Práticas Gerais
   - Sempre comentar funções e blocos complexos.
   - Evite variáveis globais desnecessárias.
   - Use -WhatIf e -Confirm antes de comandos destrutivos.
   - Mantenha scripts curtos e funções reutilizáveis.
   - Use nomes de variáveis e funções descritivos (Get-Logs, Backup-Files).

#### Documentação recomendada dentro da função
```powershell
<#
.SYNOPSIS
    Faz backup de um diretório.
.DESCRIPTION
    Copia arquivos do caminho origem para o destino informado.
.EXAMPLE
    Backup-Files -Source "C:\data" -Dest "D:\backup"
#>
```

---
### 🔹 11. Trabalhando com JSON

- Ler JSON
```powershell
$data = Get-Content "$PSScriptRoot\data.json" | ConvertFrom-Json
Write-Host "Usuário: $($data.User)"
```
- Salvar JSON
```powershell
$data.User = "Fabricio"
$data | ConvertTo-Json | Set-Content "$PSScriptRoot\data.json"
```
- 💡 PowerShell converte JSON diretamente em objetos, o que facilita automações com APIs.
---
### 🔹 12. Agendamento de Scripts (Task Scheduler)
```powershell
$action = New-ScheduledTaskAction -Execute "PowerShell.exe" -Argument "-File `"$PSScriptRoot\script.ps1`""
$trigger = New-ScheduledTaskTrigger -Daily -At 9am
Register-ScheduledTask -Action $action -Trigger $trigger -TaskName "MeuScriptDiario"
```
---
### 🔹 13. Comandos Úteis de Sistema e Rede
```powershell
Get-Service | Where-Object {$_.Status -eq 'Running'}
Test-Connection google.com -Count 2
Get-Process | Sort-Object CPU -Descending | Select-Object -First 5
Get-EventLog -LogName Application -Newest 5
```
- 💡 Test-Connection é o equivalente PowerShell para ping.
---
### 🔹 14. Execução de Comandos Externos
```powershell
$gitStatus = git status | Out-String
Write-Host $gitStatus
```
- 💡Use Out-String quando quiser armazenar a saída de comandos externos em texto.
---
### 🔹 15. Dicas de Produtividade
```powershell
    Tab completion: pressione Tab para completar comandos e parâmetros.

    Aliases comuns:

        ls = Get-ChildItem

        cat = Get-Content

        rm = Remove-Item

    Histórico: Get-History, Invoke-History, Clear-History

    Personalização: Edite $PROFILE para carregar funções e aliases automaticamente.
```

- Exemplo:
```powershell
notepad $PROFILE

Adicione dentro:

Set-Alias ll Get-ChildItem
function reload-profile { . $PROFILE }
```
--- 
### 🔹 16. Dicas Avançadas e Conceituais
- Tudo é Objeto: Diferente do CMD, PowerShell trabalha com objetos .NET.
- Pipelines reais: Os dados fluem entre comandos como objetos, não texto.
- Modularização: Divida seu projeto em pastas por tipo (funções, utilitários, setup).
- Controle de escopo: Prefira funções com variáveis locais — evite globais.
- Logs automáticos:
```powershell
function Write-Log {
    param($message)
    $timestamp = Get-Date -Format "yyyy-MM-dd HH:mm:ss"
    "$timestamp - $message" | Out-File -FilePath "$PSScriptRoot\log.txt" -Append
}
```
---
### 🔹 17. Estrutura Recomendada de Projeto Pessoal
```powershell
meus-scripts/
│
├── main.ps1
├── scripts/
│   ├── core/
│   │   ├── util.ps1
│   │   └── io.ps1
│   ├── windows/
│   └── wsl/
└── data/
```
- No main.ps1:
```powershell
$basePath = "$PSScriptRoot\scripts"
Get-ChildItem -Path $basePath -Filter *.ps1 -Recurse | ForEach-Object { . $_.FullName }
```
- Assim todos os scripts e funções ficam disponíveis automaticamente.
---
### 🔹 18. Conclusão

- PowerShell é poderoso para automações pessoais e profissionais.
Domine:

    - Manipulação de arquivos e diretórios
    - Uso de pipelines e objetos
    - Modularização de funções
    - Tratamento de erros com try/catch
    - Splatting e boas práticas de nomeação

- 💡 Sempre teste scripts com -WhatIf, comente código, e use $PSScriptRoot para garantir compatibilidade.
---
## 🔹 19. Operadores de Comparação
- No PowerShell, comparações **não usam `==`** (como em outras linguagens), e sim **operadores verbais**.  
  Isso torna o código mais legível e expressivo.

| Tipo de Comparação | Operador | Exemplo | Resultado |
|--------------------|-----------|----------|------------|
| Igual              | `-eq`     | `$x -eq 10` | Verdadeiro se `$x` for igual a 10 |
| Diferente          | `-ne`     | `$x -ne 10` | Verdadeiro se `$x` for diferente de 10 |
| Maior que          | `-gt`     | `$x -gt 5`  | Verdadeiro se `$x` for maior que 5 |
| Menor que          | `-lt`     | `$x -lt 5`  | Verdadeiro se `$x` for menor que 5 |
| Maior ou igual     | `-ge`     | `$x -ge 10` | Verdadeiro se `$x` ≥ 10 |
| Menor ou igual     | `-le`     | `$x -le 3`  | Verdadeiro se `$x` ≤ 3 |

```powershell
$currentData = @{ isFirstExec = 1 }

if ($currentData.isFirstExec -eq 1) {
    Write-Host "Primeira execução detectada."
} else {
    Write-Host "Execução subsequente."
}
```
    💡 Dica: Se o valor vier de um JSON (string "1"), converta com [int]$valor antes de comparar:

```powershell
if ([int]$currentData.isFirstExec -eq 1) { ... }
```
---
### 🔹 20. Declaração de Parâmetros com param()

- Um script ou função PowerShell deve conter apenas um bloco param().
Nele, você lista todos os parâmetros, separados por vírgulas.
Vários blocos param() são inválidos e apenas o primeiro será considerado.

✅ Correto:
```powershell
param(
    [string]$PromptMessage = "Digite o nome do usuário:",
    [string]$DataFilePath
)
Write-Host $PromptMessage
Write-Host "Arquivo: $DataFilePath"

```
❌ Errado:
```powershell
param([string]$PromptMessage)
param([string]$DataFilePath)
```
    💡 Boas práticas:

- Coloque o bloco param() no início do script.
- Use [Parameter(Mandatory = $true)] para tornar um argumento obrigatório.
- Combine com validações para maior robustez.
```powershell
param(
    [Parameter(Mandatory = $true)]
    [ValidateNotNullOrEmpty()]
    [string]$DataFilePath,

    [string]$PromptMessage = "Digite o nome do usuário:"
)

Write-Host "Iniciando script com arquivo: $DataFilePath"
```
---
### 🔹 21. JSON no PowerShell: Criar, Reescrever e Atualizar

- No PowerShell, arquivos JSON são convertidos para objetos usando `ConvertFrom-Json`.
- Por padrão, o JSON vira um **PSCustomObject**, que não aceita criar novas propriedades dinamicamente se elas não existirem.

```powershell
# Exemplo de leitura
$data = Get-Content "config.json" | ConvertFrom-Json
# Se config.json só tem {"isFirstExec":1}, $data.username = "fab" gera erro
```
- 💡 Problema comum: tentar adicionar uma chave nova diretamente a um PSCustomObject vindo de JSON.

---
### 🔹 22. Usando Hashtable para manipular JSON dinamicamente

- Convertendo para hashtable, você pode adicionar novas chaves livremente, mantendo as existentes.
```powershell
# Lê o JSON como hashtable
$data = Get-Content "config.json" | ConvertFrom-Json -AsHashtable

# Adiciona ou atualiza chave
$data["username"] = "fab"

# Salva de volta
$data | ConvertTo-Json | Set-Content "config.json"
```
- Resultado: qualquer chave anterior é preservada, e você consegue adicionar novas sem erro.

---
### 🔹 23. Adicionando propriedades dinamicamente em PSCustomObject

- Se preferir manter o PSCustomObject, use Add-Member -Force:
```powershell
$data = Get-Content "config.json" | ConvertFrom-Json

# Adiciona nova propriedade
Add-Member -InputObject $data -NotePropertyName "username" -NotePropertyValue "fab" -Force

# Salva novamente
$data | ConvertTo-Json | Set-Content "config.json"
```
- Force garante que a propriedade seja criada mesmo se não existisse antes.

---
### 🔹 24. Criando JSON do zero

- Útil se você quer garantir uma estrutura limpa, sem depender do que já existe.
```powershell
$data = @{
    isFirstExec = 1
    username    = "fab"
    theme       = "dark"
}
# Salva JSON
$data | ConvertTo-Json | Set-Content "config.json"
```
- 💡 Bom para inicialização de arquivos de configuração.
---
### 🔹 25. Estrutura recomendada para arquivos JSON de configuração

- Para armazenar múltiplas chaves do tipo dicionário (chave: valor):
```powershell
{
  "isFirstExec": 0,
  "username": "Fabricio",
  "lastRunDate": "2025-10-27T17:00:00",
  "theme": "dark"
}
```
- Cada chave é independente e pode ser adicionada/atualizada dinamicamente sem reescrever o restante.
---
### 🔹 26. Função genérica para atualizar JSON de forma segura
```powershell
function Update-JsonFile {
    param(
        [string]$Path,
        [hashtable]$NewData
    )

    if (Test-Path $Path) {
        try {
            $data = Get-Content $Path -Raw | ConvertFrom-Json -AsHashtable
        } catch {
            Write-Warning "⚠️ JSON inválido ou arquivo vazio. Criando novo."
            $data = @{}
        }
    } else {
        $data = @{}
    }

    # Atualiza ou adiciona chaves
    foreach ($key in $NewData.Keys) {
        $data[$key] = $NewData[$key]
    }

    # Salva de volta
    $data | ConvertTo-Json -Depth 10 | Set-Content $Path
}
```
```powershell
# Uso:
Update-JsonFile -Path "config.json" -NewData @{ username = "fab"; theme = "dark" }
```
- ✅ Mantém todas as chaves anteriores e adiciona novas de forma segura.

- 💡 Pode ser usada para qualquer arquivo JSON de configuração que precise de updates incrementais.
