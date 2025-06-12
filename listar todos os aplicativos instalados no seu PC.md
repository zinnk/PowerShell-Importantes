Você pode listar todos os aplicativos instalados no seu PC com Windows e salvar essa lista em um arquivo `.txt` usando o **PowerShell**. Aqui estão dois métodos: um para programas instalados para o usuário/sistema via Windows Installer (MSI), e outro para apps modernos da Microsoft Store.

---

### ✅ **1. Para programas tradicionais (instalados via MSI/EXE):**

Abra o **PowerShell como Administrador** e digite:

```powershell
Get-ItemProperty HKLM:\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*, HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\* |
Select-Object DisplayName, DisplayVersion, Publisher, InstallDate |
Where-Object { $_.DisplayName } |
Sort-Object DisplayName |
Out-File "$env:USERPROFILE\Desktop\apps_instalados.txt"
```

Esse comando:

* Acessa o registro do Windows onde os apps são listados.
* Filtra apenas os que têm um nome visível.
* Salva o resultado em um `.txt` na **Área de Trabalho** (`apps_instalados.txt`).

---

### ✅ **2. Para apps da Microsoft Store:**

No PowerShell, digite:

```powershell
Get-AppxPackage |
Select-Object Name, PackageFullName |
Out-File "$env:USERPROFILE\Desktop\apps_store.txt"
```

---

### ✅ **3. Se quiser tudo em um único `.txt`:**

```powershell
"=== PROGRAMAS TRADICIONAIS ===" | Out-File "$env:USERPROFILE\Desktop\todos_os_apps.txt"
Get-ItemProperty HKLM:\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*, HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\* |
Where-Object { $_.DisplayName } |
Select-Object DisplayName, DisplayVersion, Publisher, InstallDate |
Sort-Object DisplayName |
Out-File "$env:USERPROFILE\Desktop\todos_os_apps.txt" -Append

"`n=== APPS DA MICROSOFT STORE ===" | Out-File "$env:USERPROFILE\Desktop\todos_os_apps.txt" -Append
Get-AppxPackage |
Select-Object Name, PackageFullName |
Out-File "$env:USERPROFILE\Desktop\todos_os_apps.txt" -Append
```

---

Se quiser, posso gerar um `.ps1` com isso pronto para você rodar — é só pedir!
