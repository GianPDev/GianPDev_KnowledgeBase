### Copy all files with subdirectories (no empty)
```powershell
robocopy /S C:\SOURCE F:\BACKUP 
```
for network drives:
```powershell
robocopy /S C:\SOURCE \\SERVERNAME\home\admin\BACKUP\
```