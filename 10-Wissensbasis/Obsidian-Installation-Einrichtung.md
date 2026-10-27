---
title: Obsidian Installation & Einrichtung
created: 2026-10-27
updated: 2026-10-27
tags:
  - installation
  - obsidian
  - windows
  - einrichtung
status: active
---

# Obsidian Installation & Einrichtung

## Zweck

Schritt-für-Schritt-Installation von Obsidian unter Windows und erstmalige Einrichtung des VaultPilot-Vaults (Ergänzung zu Phase A, Teilziel 1 aus CONCEPT.md).

Obsidian ist eine kostenlose (privat genutzte) Notiz-App, die lokal auf Markdown-Dateien arbeitet – genau deshalb passt sie zu einem Git-versionierten Vault: **Die Notizen sind normale Dateien, Obsidian ist nur die Ansicht darauf.**

## Voraussetzungen

- Windows, PowerShell
- VaultPilot-Repository lokal vorhanden und über `$env:VAULTPILOT` erreichbar (Einrichtung der Variable: siehe README bzw. Checkliste A.2)

## Schritte

### 1. Obsidian installieren

**Variante 1 – über scoop (konsistent mit OpenCode-Installation):**

```powershell
scoop bucket add extras
scoop install obsidian
```

**Variante 2 – offizieller Installer:**

1. https://obsidian.md aufrufen
2. „Download" → Windows-Installer herunterladen und ausführen

**Variante 3 – winget:**

```powershell
winget install Obsidian.Obsidian
```

### 2. Version ermitteln

```powershell
scoop list obsidian
# oder in Obsidian: Einstellungen → „Über" → Version
```

### 3. VaultPilot als Vault öffnen

Ein **Vault** in Obsidian ist ein gewöhnlicher Ordner; seine Einstellungen liegen im Unterordner `.obsidian/` (in diesem Repo versioniert bzw. teils ignoriert – siehe [[90-Index/Sitzungen/2026-10-27 Git-Ignore-Arbeitsplatzkonfiguration]]).

1. Obsidian starten
2. Startbildschirm: **„Ordner als Vault öffnen"** (Open folder as vault)
3. Ordner `$env:VAULTPILOT` auswählen (Standardort: `$env:USERPROFILE\Projects\VaultPilot`)
4. Bestätigen: Obsidian fragt nach „Trust author" – bei eigenem Vault bestätigen
5. Prüfen: Ordner `00-Inbox/`, `10-Wissensbasis/`, `90-Index/` sind in der linken Seitenleiste sichtbar

**Hinweis:** Nicht „Create new vault" wählen – das würde einen leeren Vault anlegen statt den bestehenden zu öffnen.

### 4. Grundkonfiguration prüfen

Die geteilte Vault-Konfiguration liegt versioniert im Repo:

- `.obsidian/app.json`, `appearance.json` – Editor-Verhalten, Theme (aktuell: Solarized)
- `.obsidian/core-plugins.json`, `community-plugins.json` – aktivierte Plugins
- `.obsidian/daily-notes.json` – Daily Notes landen in `00-Inbox/`

Falls gewünscht: Theme und Basis-Optionen prüfen (Einstellungen → Appearance / Editor). Details zur Auswertungs-Konfiguration: [[10-Wissensbasis/Obsidian-Auswertung-Einrichten]].

## Verifikation

Nach erfolgreichem Abschluss:

- `scoop list obsidian` zeigt die installierte Version (oder Installer-Variante: Obsidian startet)
- Obsidian öffnet den VaultPilot-Ordner als Vault
- Die Ordnerstruktur `00-Inbox/`, `10-Wissensbasis/`, `90-Index/` ist sichtbar
- Notizen lassen sich öffnen und rendern (z. B. `10-Wissensbasis/Konzept.md`)

## Links

- [[10-Wissensbasis/Obsidian-Grundlagen]] – nächste Lektüre: Bedienung
- [[10-Wissensbasis/Phase-A-Installation]] – OpenCode-Installation
- [[10-Wissensbasis/Obsidian-Auswertung-Einrichten]] – Auswertungs-Setup (Phase C)
- [[90-Index/Entwicklungsprotokoll]]
- [[10-Wissensbasis/Umsetzung-Checkliste]]
