---
title: Umsetzung – Checkliste
created: 2026-10-26
updated: 2026-10-27
tags:
  - umsetzung
  - checklist
  - opencode
  - obsidian
status: active
---

# Umsetzung – Checkliste

## Zweck

Konkrete Aufgabenliste für die Umsetzungsphase des VaultPilot-Projekts (laut CONCEPT.md Teilziele 1–4). Wird schrittweise abgearbeitet.

## Phase A: Installation & Setup (Teilziel 1)

### A.1 OpenCode über PowerShell + scoop installieren

- [ ] PowerShell als normaler User öffnen (kein Administrator nötig für CurrentUser-Scope)
- [ ] Scoop installieren:
  ```powershell
  Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
  Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
  ```
- [ ] OpenCode Version 2 über scoop installieren:
  ```powershell
  scoop install git
  scoop bucket add versions
  scoop install versions/opencode2
  ```
- [ ] Version prüfen:
  ```powershell
  opencode --version
  ```
- [ ] Modell prüfen/wechseln (Hinweis: es gibt keinen CLI-Befehl `opencode model`; verfügbare Modelle auflisten mit `opencode models`, Wechsel über TUI `Ctrl+X` → `m`)
  ```powershell
  opencode models
  ```

### A.2 Projektrepository klonen / öffnen

- [ ] Pfad-Variable einrichten (einmalig, dauerhaft für den Benutzer; Einrichtung im Detail siehe README):
  ```powershell
  [Environment]::SetEnvironmentVariable("VAULTPILOT", "$env:USERPROFILE\Projects\VaultPilot", "User")
  $env:VAULTPILOT = "$env:USERPROFILE\Projects\VaultPilot"   # aktuelle Sitzung (oder PowerShell neu starten)
  ```
- [ ] Repository klonen (falls auf einem anderen Rechner; Standardort: `$env:USERPROFILE\Projects\VaultPilot`):
  ```powershell
  git clone https://github.com/fdoebbelin/VaultPilot.git $env:VAULTPILOT
  cd $env:VAULTPILOT
  ```
- [ ] Oder bestehendes Verzeichnis öffnen:
  ```powershell
  cd $env:VAULTPILOT
  ```

> **Konvention:** In allen Leitfäden wird das Repository über `$env:VAULTPILOT` adressiert – niemals über hartcodierte Benutzerpfade.

### A.3 Obsidian installieren und Vault öffnen

Leitfaden: [[10-Wissensbasis/Obsidian-Installation-Einrichtung]]

- [ ] Obsidian installieren (Variante 1, konsistent mit OpenCode):
  ```powershell
  scoop bucket add extras
  scoop install obsidian
  ```
  (Alternativ: Installer von https://obsidian.md oder `winget install Obsidian.Obsidian`)
- [ ] VaultPilot-Ordner als Vault öffnen (nicht „Create new vault")
- [ ] Prüfen: `00-Inbox/`, `10-Wissensbasis/`, `90-Index/` sichtbar
- [ ] Grundkonfiguration geladen (Theme, aktivierten Plugins, Daily-Notes-Speicherort)

> **Verifiziert am 2026-10-27 (dieser Rechner):** Installation via offiziellem Installer (Variante 2) unter `%LOCALAPPDATA%\Programs\Obsidian\Obsidian.exe`; Vault als geöffnet registriert in `%APPDATA%\obsidian\obsidian.json`; Theme Solarized geladen (siehe Commit `13516da`).

## Phase B: Erster Workflow-Test (Teilziel 3)

### B.1 Agent & Command prüfen

- [ ] VaultPilot-Agent geladen:
  ```powershell
  opencode agent list
  # erwartet: vaultpilot in der Liste
  ```
- [ ] Commands verfügbar:
  ```powershell
  opencode command list
  # erwartet: vault-new, vault-link, vault-index
  ```

### B.2 Erste Wissensnotiz erstellen

- [ ] `/vault-new "Erster Test: Wie funktioniert ein KI-Agent?"` ausführen
- [ ] Prüfen: Notiz wurde in `10-Wissensbasis/` angelegt?
- [ ] Prüfen: Frontmatter (`title`, `tags`, `created`, `updated`) vorhanden?
- [ ] Prüfen: `[[Wikilinks]]` korrekt gesetzt?

### B.3 Notiz vernetzen

- [ ] `/vault-link "10-Wissensbasis/Erster Test: Wie funktioniert ein KI-Agent?"` ausführen
- [ ] Prüfen: Verknüpfung zu `[[VaultPilot – Konzept]]` oder verwandten Notizen ergänzt?

### B.4 Wissensindex aktualisieren

- [ ] `/vault-index "Allgemeiner Überblick"` ausführen
- [ ] Prüfen: MOC in `90-Index/` erstellt/aktualisiert? → [[90-Index/Wissensindex]] (2026-10-27 erstellt, verlinkt alle Kernnotizen)

## Phase C: Obsidian als Auswertungsfläche (Teilziel 4)

### C.0 Obsidian-Grundlagen erarbeiten

Leitfaden mit Übungen: [[10-Wissensbasis/Obsidian-Grundlagen]] · Abarbeitungsnachweis: [[00-Inbox/Übung Obsidian-Grundlagen]]

- [ ] Oberfläche bekannt: Seitenleisten, Tabs, Panes, Statusleiste *(via `workspace.json` belegt)*
- [ ] Tastenkürzel getestet: `Strg+P`, `Strg+O`, `Strg+Shift+F`, `Strg+E` *(Nutzerübung 2026-10-27, in Übungsnotiz abgehakt)*
- [ ] Markdown-Grundlagen und Frontmatter verstanden *(Leitfaden + Teilnehmernotiz erstellt)*
- [ ] `[[Wikilink]]` gesetzt und Backlinks geprüft *(Teilnehmernotiz mit 3 Links; Backlinks-Pane aktiv)*
- [ ] Graph-Ansicht betrachtet *(Nutzerübung 2026-10-27; `graph.json` angelegt)*
- [ ] Sync-Regeln für Git-Vault bekannt (pull vor / push nach Sitzung) *(dokumentiert in [[10-Wissensbasis/Git-Grundlagen]])*

### C.1 Vault in Obsidian öffnen

- [ ] Obsidian starten und VaultPilot-Vault öffnen: `$env:VAULTPILOT`
- [ ] Prüfen: Ordner `00-Inbox/`, `10-Wissensbasis/`, `90-Index/` sichtbar

### C.2 Core-Plugins aktivieren

- [ ] Einstellungen → Core Plugins
- [ ] `Daily Notes` aktiviert (verifiziert via `core-plugins.json`)
- [ ] `Templates` aktiviert
- [ ] `Backlinks` aktiviert
- [ ] Daily Notes Speicherort auf `00-Inbox` setzen (verifiziert via `daily-notes.json`)

### C.3 Erste Daily Note erstellen und verknüpfen

- [ ] Erste Daily Note erstellen (Strg+P → „Tagesnotiz erstellen")
- [ ] Prüfen: Wurde in `00-Inbox/` abgelegt? (laut `daily-notes.json`)
- [ ] Daily Note per `[[Wikilink]]` mit einer Wissensnotiz verknüpfen (z. B. `[[Erster-Workflow-Test]]`)
- [ ] Backlinks prüfen (Seitenleiste → Backlinks) *(via `workspace.json` verifiziert: „Rückverweise"-Pane aktiv eingerichtet)*

## Phase D: Dokumentation & Commit

### D.1 Sessionprotokoll erstellen

- [ ] Sessionprotokoll als `JJJJ-MM-TT Umsetzung <Thema>.md` in `90-Index/Sitzungen/` anlegen
- [ ] Vorlage `[[90-Index/Sessionprotokoll-Vorlage]]` verwenden
- [ ] Probleme, Lösungen, Artefakte dokumentieren

### D.2 Zentrales Entwicklungsprotokoll aktualisieren

- [ ] Neue Zeile in Sitzungstabelle von `[[90-Index/Entwicklungsprotokoll]]` eintragen
- [ ] Aktueller Handoff-Block aktualisieren

### D.3 Commit & Push

- [ ] `git add -A`
- [ ] `git commit -m "..."`
- [ ] `git push -u origin main`

## Nächste Schritte nach Abschluss

- [ ] Konzept finalisieren → CONCEPT.md v2, Status final (M1 ✅, 2026-10-27)
- [ ] Wissensbasis auf 5–7 Kernnotizen ausbauen (K2) → [[KI-Agent-vs-Chat]], [[Agenten-Workflow]], [[10-Wissensbasis/Phase-A-Installation]], [[10-Wissensbasis/Git-Grundlagen]], [[10-Wissensbasis/Obsidian-Grundlagen]] (+ Hilfsnotizen), MOC: [[90-Index/Wissensindex]] (K3)
- [ ] C.0-Rest: Tastenkürzel testen + Graph-Ansicht betrachten (Nutzerübung 2026-10-27, Nachweis: [[00-Inbox/Übung Obsidian-Grundlagen]])
- [ ] Abschlussbericht finalisieren (2026-10-27)

**Alle Phasen A–D abgeschlossen (2026-10-27). Alle Erfolgskriterien K1–K6 erfüllt.**
