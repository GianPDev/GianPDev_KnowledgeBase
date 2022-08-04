### Easy way to search and get packages
https://winget.run
Can click `+` to add to downloads and copy oneliner

### My App Oneliner 
Must open windows store > ... > Downloads and updates > App Installer 
Winget oneliner (working as of 2022-08-04, 5-6GB)
```powershell
winget install Microsoft.WindowsTerminal.Preview; winget install Microsoft.PowerShell; winget install Git.Git; winget install ShiningLight.OpenSSL; winget install neovim; winget install libreoffice; winget install Zeit.Hyper; winget install GnuPG; winget install Nvidia.Broadcast; winget install -e --id Obsidian.Obsidian;winget install -e --id Discord.Discord;winget install -e --id Valve.Steam;winget install -e --id EpicGames.EpicGamesLauncher;winget install -e --id M2Team.NanaZip.Preview; winget install synctrayzor; winget install TechPowerUp.NVCleanstall; winget install VB-Audio.Voicemeeter.Potato; winget install audacium; winget install Microsoft.VisualStudioCode; winget install NoMachine.NoMachine; winget install ShareX.ShareX; winget install Parsec.Parsec
```
Use [winrice](https://github.com/pratyakshm/WinRice/blob/main/doc/Main-brief.md) uninstall bloat and other windows telemetry things:
```powershell
Invoke-WebRequest bit.ly/WinRice | Invoke-Expression
```