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

### 4. Verfügbare Modelle auflisten

```powershell
opencode models
```

**Hinweis:** Es gibt keinen CLI-Befehl `opencode model` (Einzahl) zum Anzeigen/Wechseln des aktuellen Modells. Der Befehl existiert nicht in dieser Form unter OpenCode v2.

**Modell wechseln / anzeigen:**
- Über die **OpenCode TUI**: Leader-Key `Ctrl+X` → `m` → Modell auswählen
- Über die OpenCode-Konfigurationsdatei: `~/.config/opencode/config.json` bzw. Projekt-Config
- Verfügbare Modelle auflisten: `opencode models`

## Verifikation

Nach erfolgreichem Abschluss:
- `opencode --version` zeigt die installierte Version
- OpenCode lässt sich starten (`opencode`)
- Aktives Modell ist in der TUI einstellbar (z. B. `opencode/nemotron-3.5-super-vl-free`)

## Links

- [[90-Index/Entwicklungsprotokoll]]
- [[10-Wissensbasis/Umsetzung-Checkliste]]
