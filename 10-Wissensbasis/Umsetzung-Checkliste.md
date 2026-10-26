---
title: Umsetzung – Checkliste
created: 2026-10-26
updated: 2026-10-26
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

### C.1 Vault in Obsidian öffnen

- [ ] Obsidian starten
- [ ] Vault öffnen: `C:\Users\fritz\Projects\VaultPilot`
- [ ] Prüfen: Ordner `00-Inbox/`, `10-Wissensbasis/`, `90-Index/` sichtbar?

### C.2 Core-Plugins aktivieren

- [ ] Einstellungen → Core Plugins
- [ ] `Daily Notes` aktiviert
- [ ] `Templates` aktiviert
- [ ] `Backlinks` aktiviert

### C.3 Erste Daily Note erstellen

- [ ] Daily Note über Obsidian-Befehl erstellen
- [ ] Prüfen: Wurde in `00-Inbox/` abgelegt? (laut `daily-notes.json`)

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
