Day 1: https://github.com/KloudKraft-in/hcl_nov26/blob/main/Day1/Lab%201.1_%20Create%20an%20Azure%20Functions%20App.pdf
Day 2: https://github.com/KloudKraft-in/hcl_nov26/blob/main/Day2/Lab%202.1_%20Timer-Triggered%20Stale%20Order%20Sweep.md


Lab1.2 prereuisite of installation

Write-Host "=== Prerequisites Readiness Check ===" -ForegroundColor Cyan
Write-Host "1. .NET SDK Version:" -NoNewline
dotnet --version

Write-Host "2. Azure Functions Core Tools Version:" -NoNewline
func --version

Write-Host "3. VS Code CLI Version:" -NoNewline
code --version

Write-Host "4. VS Code Extensions:" -ForegroundColor Yellow
code --list-extensions | Select-String "csdevkit|rest-client"


##install .net SDK

[Net.ServicePointManager]::SecurityProtocol = 3072
Invoke-WebRequest -Uri "https://dot.net/v1/dotnet-install.ps1" -OutFile "$env:TEMP\dotnet-install.ps1"
& "$env:TEMP\dotnet-install.ps1" -Channel 10.0 -InstallDir "C:\Program Files\dotnet"

$env:Path += ";C:\Program Files\dotnet"
dotnet --version
