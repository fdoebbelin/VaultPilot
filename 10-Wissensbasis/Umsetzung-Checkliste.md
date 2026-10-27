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

- [ ] Repository klonen (falls auf einem anderen Rechner):
  ```powershell
  git clone https://github.com/fdoebbelin/VaultPilot.git
  cd VaultPilot
  ```
- [ ] Oder bestehendes Verzeichnis öffnen:
  ```powershell
  cd C:\Users\fritz\Projects\VaultPilot
  ```

### A.3 Obsidian installieren und Vault öffnen

Leitfaden: [[10-Wissensbasis/Obsidian-Installation-Einrichtung]]

- [x] Obsidian installieren (Variante 1, konsistent mit OpenCode):
  ```powershell
  scoop bucket add extras
  scoop install obsidian
  ```
  (Alternativ: Installer von https://obsidian.md oder `winget install Obsidian.Obsidian`)
- [x] VaultPilot-Ordner als Vault öffnen (nicht „Create new vault")
- [x] Prüfen: `00-Inbox/`, `10-Wissensbasis/`, `90-Index/` sichtbar
- [x] Grundkonfiguration geladen (Theme, aktivierten Plugins, Daily-Notes-Speicherort)

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
- [ ] Prüfen: MOC in `90-Index/` erstellt/aktualisiert?

## Phase C: Obsidian als Auswertungsfläche (Teilziel 4)

### C.0 Obsidian-Grundlagen erarbeiten

Leitfaden mit Übungen: [[10-Wissensbasis/Obsidian-Grundlagen]]

- [ ] Oberfläche bekannt: Seitenleisten, Tabs, Panes, Statusleiste
- [ ] Tastenkürzel getestet: `Strg+P`, `Strg+O`, `Strg+Shift+F`, `Strg+E`
- [ ] Markdown-Grundlagen und Frontmatter verstanden
- [ ] `[[Wikilink]]` gesetzt und Backlinks geprüft
- [ ] Graph-Ansicht betrachtet
- [ ] Sync-Regeln für Git-Vault bekannt (pull vor / push nach Sitzung)

### C.1 Vault in Obsidian öffnen

- [x] Obsidian starten und VaultPilot-Vault öffnen: `C:\Users\fritz\Projects\VaultPilot`
- [x] Prüfen: Ordner `00-Inbox/`, `10-Wissensbasis/`, `90-Index/` sichtbar

### C.2 Core-Plugins aktivieren

- [x] Einstellungen → Core Plugins
- [x] `Daily Notes` aktiviert (verifiziert via `core-plugins.json`)
- [x] `Templates` aktiviert
- [x] `Backlinks` aktiviert
- [x] Daily Notes Speicherort auf `00-Inbox` setzen (verifiziert via `daily-notes.json`)

### C.3 Erste Daily Note erstellen und verknüpfen

- [x] Erste Daily Note erstellen (Strg+P → „Tagesnotiz erstellen")
- [x] Prüfen: Wurde in `00-Inbox/` abgelegt? (laut `daily-notes.json`)
- [x] Daily Note per `[[Wikilink]]` mit einer Wissensnotiz verknüpfen (z. B. `[[Erster-Workflow-Test]]`)
- [ ] Backlinks prüfen (Seitenleiste → Backlinks)

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

- [ ] Konzept finalisieren (Outcome, Meilensteine, Erfolgskriterien präzisieren)
- [ ] Weitere Wissensnotizen für Kursinhalte erstellen
- [ ] Obsidian als zentrale Auswertungsfläche nutzen
