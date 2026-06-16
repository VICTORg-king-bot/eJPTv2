# Hotfixes en Windows

Los hotfixes son parches de seguridad instalados en Windows. Enumerarlos ayuda a identificar vulnerabilidades no parcheadas.

## Listar Hotfixes con PowerShell

```powershell
Get-HotFix
```

## Contar Hotfixes Instalados

```powershell
(Get-HotFix).Count
```

## Listar Hotfixes con WMIC

```cmd
wmic qfe list brief /format:table
```

> Si faltan parches de seguridad importantes (como MS17-010 para EternalBlue), el sistema es vulnerable.
