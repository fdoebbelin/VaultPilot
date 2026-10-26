---
title: Phase A – Installation OpenCode via Scoop
created: 2026-10-26
updated: 2026-10-26
tags:
  - installation
  - scoop
  - opencode
  - powershell
  - windows
status: active
---

# Phase A – Installation OpenCode via Scoop

## Voraussetzungen

- Windows, PowerShell
- Ausführung als **normaler User** (kein Administrator erforderlich für scoop im CurrentUser-Scope)

## Schritte

### 1. Scoop installieren

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
```

### 2. OpenCode Version 2 installieren

```powershell
scoop install git
scoop bucket add versions
scoop install versions/opencode2
```

### 3. Version ermitteln

```powershell
opencode --version
```

### 4. Aktives Modell prüfen

```powershell
opencode model
```

**Fehler aufgetreten:**
```text
Error: ENOENT: no such file or directory, chdir 'C:\Users\fritz\Projects\VaultPilot' -> 'model'
    at chdir (unknown)
    at <anonymous> (B:/~BUN/root/chunk-v76hw3dq.js:95:6479)
```

**Ursache:** Unbekannt – wahrscheinlich ein CLI-Bug oder der Befehl `model` existiert nicht in dieser Form unter OpenCode v2.

**Workaround / Lösung:**
- Modell über die **OpenCode TUI** auswählen (Leader-Key `Ctrl+X` → `m`)
- Oder Modell direkt in der OpenCode-Konfigurationsdatei setzen (`~/.config/opencode/config.json` bzw. Projekt-Config)
- Alternativ: `opencode model list` (falls verfügbar) oder `opencode models` prüfen

## Verifikation

Nach erfolgreichem Abschluss:
- `opencode --version` zeigt die installierte Version
- OpenCode lässt sich starten (`opencode`)
- Aktives Modell ist `opencode/nemotron-3.5-super-vl-free` (bzw. anderes gewünschtes Modell)

## Links

- [[90-Index/Entwicklungsprotokoll]]
- [[10-Wissensbasis/Umsetzung-Checkliste]]
