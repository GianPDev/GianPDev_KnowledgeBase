### Recommended JDK/JRE installer
Using https://whichjdk.com/ advice, use Adoptium Eclipse Temurin 17.0.3 or higher
```powershell
winget install EclipseAdoptium.Temurin.17.JDK
```

### To run jnlp files
Requires javaws.exe, which is Java Web Start, it was deprecated in Java 9 and removed in Java 11.
Download it here: https://github.com/karakun/OpenWebStart
OR
```powershell
winget install karakun.OpenWebStart
```
This will install a program that will auto install the required files to run the jnlp file.