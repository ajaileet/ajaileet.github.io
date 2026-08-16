# Grep Equivalents in Windows

## Command Prompt — `findstr`

```
findstr /s /i "user" *.*
```

| Flag | Description |
|------|-------------|
| `/s` | Recursive (search subdirectories) |
| `/i` | Case-insensitive |
| `/r` | Use regular expressions |
| `/n` | Show line numbers |
| `/m` | Show only filenames that match |

### Examples

```
findstr /s /i /n "password" *.txt
findstr /s /r "error[0-9]" *.log
findstr /s /m "TODO" *.*
```

## PowerShell — `Select-String`

```powershell
Get-ChildItem -Recurse | Select-String "user"
```

Short form:

```powershell
gci -r | sls "user"
```

### Useful variations

```powershell
# Filter by file type
gci -r -Include *.log,*.txt | sls "user"

# Case-sensitive (default is case-insensitive)
gci -r | sls "user" -CaseSensitive

# Show only filenames
gci -r | sls "user" | Select-Object -Unique Path

# Regex pattern
gci -r | sls -Pattern "error\d+"

# Context lines (like grep -A and -B)
gci -r | sls "user" -Context 2,2
```

## WSL (Windows Subsystem for Linux)

If WSL is installed, use grep directly:

```bash
grep -ri "user" .
grep -rn "user" --include="*.txt" .
```
