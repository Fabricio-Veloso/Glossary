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
