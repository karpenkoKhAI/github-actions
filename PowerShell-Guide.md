# PowerShell in GitHub Actions - Troubleshooting Guide

## Why You Weren't Seeing Output

### Issue 1: Wrong Operating System
```yaml
# ❌ This won't work for PowerShell commands
runs-on: ubuntu-latest  # Uses bash by default

# ✅ Use this for full PowerShell support
runs-on: windows-latest
```

### Issue 2: Missing Shell Configuration
```yaml
# ❌ Without shell specification, uses system default
run: Get-ChildItem

# ✅ Specify PowerShell shell explicitly  
shell: powershell
run: Get-ChildItem

# ✅ Or use PowerShell Core (cross-platform)
shell: pwsh
run: Get-ChildItem
```

### Issue 3: Shell Command Format
```yaml
# ❌ This format is incomplete
shell: C:\Program Files\PowerShell\7\pwsh.EXE -command ". '{0}'"

# ✅ Use the standard format instead
shell: pwsh -command ". '{0}'"
# or simply
shell: pwsh
```

## Shell Options in GitHub Actions

| Shell | Runs On | Command |
|-------|---------|---------|
| `powershell` | Windows only | Windows PowerShell 5.x |
| `pwsh` | Cross-platform | PowerShell Core 6+ |
| `pwsh -command ". '{0}'"` | Cross-platform | PowerShell with custom execution |
| `bash` | Linux/macOS/Windows | Bash shell |
| `cmd` | Windows only | Command Prompt |

## Working Examples

### Basic PowerShell Commands
```yaml
- name: List Files (PowerShell)
  shell: powershell
  run: |
    Get-ChildItem
    Get-Location
    Write-Host "Files listed successfully!"
```

### PowerShell Core (Cross-platform)
```yaml
- name: List Files (PowerShell Core)
  shell: pwsh
  run: |
    Get-ChildItem
    Get-Location  
    Write-Host "Files listed successfully!"
```

### Cake Build Example
```yaml
- name: Run Cake Build
  shell: powershell
  run: |
    # Your cake build command
    .\cake.ps1 -Configuration release -Target Release
```

## Common PowerShell Commands vs Bash

| Task | PowerShell | Bash |
|------|------------|------|
| List files | `Get-ChildItem` | `ls` |
| Current directory | `Get-Location` | `pwd` |
| Create directory | `New-Item -ItemType Directory` | `mkdir` |
| Copy files | `Copy-Item` | `cp` |
| Environment variable | `$env:VARIABLE` | `$VARIABLE` |

## Why Output Was Missing

1. **Wrong Shell**: Ubuntu runners don't have PowerShell by default
2. **Silent Failures**: Commands failed silently without proper error handling
3. **Missing Installation**: PowerShell Core needs to be installed on Linux
4. **Incorrect Syntax**: Shell configuration wasn't properly formatted

## Solution Summary

✅ **Use the new `powershell-demo.yml` workflow I created** - it shows all the working examples!
