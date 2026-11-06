# Lab 1.2 – Prerequisites Setup Guide

## New Machine Setup for: Build and Run an HTTP Function Locally

> Follow each step in order. After every installation, **close and reopen your terminal** before moving to the next step.

---

## Step 1: Install Node.js (LTS)

**Why:** Required for npm, which is used to install Azure Functions Core Tools.

1. Download from: <https://nodejs.org>
2. Select the **LTS** version (Windows Installer `.msi`, 64-bit).
3. Run the installer with default settings.
4. Close and reopen the terminal.
5. Verify:

```powershell
node --version
npm --version
```

**Expected output:** Version numbers (e.g., `v22.x.x` and `10.x.x`).

---

## Step 2: Install .NET 10 SDK

**Why:** Required for building and running C# Azure Functions.

1. Download from: <https://dotnet.microsoft.com/en-us/download/dotnet/10.0>
2. Under **SDK**, download the **Windows x64 installer** (`.exe` file).
3. Run the installer.
4. Close and reopen the terminal.
5. Verify:

```powershell
dotnet --version
```

**Expected output:** A version starting with `10.` (e.g., `10.0.100`).

## Step 3: Install Azure Functions Core Tools 4.x

**Why:** Required to create, build, run, and debug Azure Functions locally.

### Option A – Using npm (recommended)

```powershell
npm install -g azure-functions-core-tools@4
```

### Option B – Using MSI Installer (if npm is unavailable)

Download directly from: <https://go.microsoft.com/fwlink/?linkid=2174087>

Run the installer and follow the prompts.

### Verify

```powershell
func --version
```

**Expected output:** A version starting with `4.` (e.g., `4.16.0`).

---

## Step 4: Install Visual Studio Code

**Why:** The code editor used for all lab exercises.

5. Verify:

```powershell
code --version
```

**Expected output:** A version number (e.g., `1.96.x`).

---

## Step 5: Install VS Code Extensions

**Why:** These extensions provide C# language support, HTTP request testing, and local storage emulation.

Run these commands in the terminal:

```powershell
code --install-extension ms-dotnettools.csdevkit
```

```powershell
code --install-extension humao.rest-client
```

```powershell
code --install-extension azurite.azurite
```

| Extension | Identifier | Purpose |
|-----------|-----------|---------|
| C# Dev Kit | `ms-dotnettools.csdevkit` | C# language support, debugging, and project management |
| REST Client | `humao.rest-client` | Send HTTP requests from `.http` files in VS Code |
| Azurite | `azurite.azurite` | Local Azure Storage emulator |

---

## Step 6: Full Verification Script

Copy and paste this entire script into PowerShell to verify all prerequisites at once:

```powershell
Write-Host ""
Write-Host "============================================" -ForegroundColor Cyan
Write-Host "  Lab 1.2 Prerequisites Readiness Check" -ForegroundColor Cyan
Write-Host "============================================" -ForegroundColor Cyan
Write-Host ""

# 1. Node.js
Write-Host "1. Node.js Version:        " -NoNewline
try { node --version } catch { Write-Host "NOT INSTALLED" -ForegroundColor Red }

# 2. npm
Write-Host "2. npm Version:            " -NoNewline
try { npm --version } catch { Write-Host "NOT INSTALLED" -ForegroundColor Red }

# 3. .NET SDK
Write-Host "3. .NET SDK Version:       " -NoNewline
try { dotnet --version } catch { Write-Host "NOT INSTALLED" -ForegroundColor Red }

# 4. Azure Functions Core Tools
Write-Host "4. Core Tools Version:     " -NoNewline
try { func --version } catch { Write-Host "NOT INSTALLED" -ForegroundColor Red }

# 5. VS Code
Write-Host "5. VS Code Version:        " -NoNewline
try { (code --version | Select-Object -First 1) } catch { Write-Host "NOT INSTALLED" -ForegroundColor Red }

# 6. VS Code Extensions
Write-Host ""
Write-Host "6. Required VS Code Extensions:" -ForegroundColor Yellow
$extensions = code --list-extensions
$required = @(
    @{ Name = "C# Dev Kit";    Id = "ms-dotnettools.csdevkit" },
    @{ Name = "REST Client";   Id = "humao.rest-client" },
    @{ Name = "Azurite";       Id = "azurite.azurite" }
)
foreach ($ext in $required) {
    if ($extensions -match $ext.Id) {
        Write-Host "   [PASS] $($ext.Name)" -ForegroundColor Green
    } else {
        Write-Host "   [MISSING] $($ext.Name) — install with: code --install-extension $($ext.Id)" -ForegroundColor Red
    }
}

Write-Host ""
Write-Host "============================================" -ForegroundColor Cyan
Write-Host "  Check complete." -ForegroundColor Cyan
Write-Host "============================================" -ForegroundColor Cyan
```

---

## Troubleshooting

| Issue | Resolution |
|-------|-----------|
| `dotnet` not recognized | .NET SDK not installed or not in PATH. Reinstall and restart terminal. |
| `func` not recognized | Core Tools not installed or not in PATH. Reinstall via npm or MSI. |
| `npm` not recognized | Node.js not installed. Download and install from https://nodejs.org. |
| `code` not recognized | VS Code not in PATH. Reinstall with "Add to PATH" checked, or open VS Code and run `Shell Command: Install 'code' command in PATH` from the Command Palette (Ctrl+Shift+P). |
| VS Code terminal doesn't see new tools | Close VS Code completely and reopen it. VS Code caches PATH at launch. |
| PowerShell script errors | Run each line one at a time. Do not paste multiple lines together. |
| .NET install script hangs | Cancel with Ctrl+C and use the direct `.exe` installer instead. |

---

*Prepared for: Azure Serverless Training – Day 1, Lab 1.2*
