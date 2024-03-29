---
tags: [terminal, powershell, bash, path, env, environment, string, console, sed, editing, piped, object, tostring, files, hidden]
---

[[winget (official package manager)]]
[[chocolatey (package manager)]]
[[robocopy]]

#### Search directory for file (without searching within files)
```powershell
ls | Select-Object Name -ExpandProperty Name | Select-String SEARCHFILENAME
```
*If `Select-Object` was removed, it would search within text files*
```powershell
ls *.apk | ForEach-Object {echo $_.Name}
```
#### Extra: Install all apks in folder via adb
```powershell
$count=0; ls *.apk | ForEach-Object {echo "Installing: $_"; adb install $_.Name; $count++}; echo "Attempted to install $count apps."
```

#### Show hidden files when using Get-Childitem (ls, dir or gci)
```powershell
ls -Force
```

#### Print Path Environment Variables as Plain String
```powershell
ls env:Path | Select-Object -ExpandProperty Value 
```

#### Print Path Environment Variables and make it more readable
```powershell
ls env:Path | Select-Object -ExpandProperty Value | % {$_.replace(";","`n")}
```
This:
```powershell
% {$_.replace(";","`n")}
```
is very similar to using bash's [[bash utilities#Using Sed to modify files and pipe|sed]]
*Also note that newlines, return carriage etc. are done by backticks (**\`**) (This is the same button as **~**) i.e:*
```powershell
# `n for new line
# `r for return carriage
```

### Adding Firewall rule in Windows via Powershell
```powershell
New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
```

### FZF Key binds in powershell (with fzf already installed)
```powershell
# in admin powershell
Install-Module -Name PSFzf
# rest can be done in normal powershell
mkdir "C:\Users\$env:username\Documents\WindowsPowerShell"
echo "Set-PsFzfOption -PSReadlineChordProvider 'Ctrl+t' -PSReadlineChordReverseHistory 'Ctrl+r'" | Out-File -Append $profile
```

### Install Node
```powershell
scoop install fnm
echo "fnm env --use-on-cd | Out-String | Invoke-Expression" | Out-File -Append $profile
fnm install 18 # install lts 18^
```