---
title: Agenten-Workflow in VaultPilot
created: 2026-10-27
updated: 2026-10-27
tags:
  - ki-agent
  - opencode
  - workflow
  - agenten-ki
status: active
---

# Agenten-Workflow in VaultPilot

## Zweck

Wie das Agenten-Prinzip (siehe [[KI-Agent-vs-Chat]]) in VaultPilot konkret umgesetzt ist – und wie Teilnehmer den Agenten **kritisch prüfen** statt ihm blind zu folgen (Kernnotiz zu K2).

## Das Prinzip: Ziel → Plan → Tool-Use → Iteration

| Phase | Bedeutung | Beispiel im Kurs |
|---|---|---|
| **Ziel** | Auftrag präzisieren | „Erstelle eine Notiz zu Git-Grundlagen" |
| **Plan** | Agent skizziert max. ~5 Schritte | „Struktur prüfen → Notiz anlegen → verlinken → protokollieren" |
| **Tool-Use** | Agent führt Aktionen aus | Dateien lesen/schreiben, `git`-Befehle, Suche |
| **Iteration** | Ergebnis prüfen, nachbessern | `git status` bestätigt Commit; Notiz korrekt verlinkt? |

Der Unterschied zum Chat: Der Agent **führt aus** (schreibt Dateien, committet), der Chat **beschreibt nur**.

## Die Bausteine in `.opencode/`

- **`agents/vaultpilot.md`** – die Agenten-Persona: Rolle, Arbeitsweise (die 4 Phasen), Regeln (u. a. Pfad-Konvention `$env:VAULTPILOT`, keine Löschungen ohne Anfrage) und Vault-Konventionen (Ordner, Frontmatter, Tags)
- **`commands/vault-new.md`** – `/vault-new "<Thema>"`: legt eine Wissensnotiz mit Frontmatter + `[[Wikilinks]]` an
- **`commands/vault-link.md`** – `/vault-link "<Notiz>"`: vernetzt eine Notiz mit verwandten Notizen
- **`commands/vault-index.md`** – `/vault-index "<Fokus>"`: erstellt/aktualisiert den Wissensindex (MOC) in `90-Index/`
- **`commands/vault-reset.md`** – `/vault-reset check|apply`: stellt den definierten Startpunkt her (00-Inbox nur Startdokumente; Checkboxen im Arbeitsmaterial zurückgesetzt; Historie bleibt unverändert)

**Aufrufen eines Commands (so geht's):**

1. OpenCode im Vault starten: `cd $env:VAULTPILOT` → `opencode` (TUI)
2. Im Eingabefeld `/` tippen → OpenCode zeigt die verfügbaren Slash-Commands mit Autocomplete (`vault-new`, `vault-link`, `vault-index`)
3. Command mit Argument ausführen, z. B. `/vault-index Allgemeiner Überblick`
4. Der Agent arbeitet den Auftrag ab (Ziel → Plan → Tool-Use → Iteration) und meldet das Ergebnis – **verifizieren**: die betroffene Datei öffnen (z. B. `90-Index/Wissensindex.md`) und prüfen
5. Danach wie immer: `git add` → `git commit` → `git push` (siehe [[10-Wissensbasis/Git-Grundlagen]])

## Der Sitzungs-Workflow (Handoff/Pickup)

1. **Pickup:** Entwicklungsprotokoll öffnen, „Aktueller Handoff" lesen, bei offenen Punkten fortsetzen
2. **Arbeit:** Themen umsetzen – dabei Checklisten ([[10-Wissensbasis/Umsetzung-Checkliste]]) abhaken
3. **Handoff:** Sessionprotokoll in `90-Index/Sitzungen/` nach Vorlage erstellen, Tabellenzeile + Handoff-Block aktualisieren, `git add` → `commit` → `push`

Ablageort der Details: [[90-Index/Entwicklungsprotokoll]].

## Kritische Würdigung: Agenten-Aussagen prüfen

Agenten sind fehleranfällig (Planung, Tool-Use) – deshalb gilt „Vertrauen durch Verifikation":

- **Behauptungen gegen Gegenbeweise prüfen:** „ gepusht" → selbst `git status` ausführen; „Notiz erstellt" → Datei öffnen
- **Diffs lesen:** `git diff` zeigt, was der Agent wirklich geändert hat
- **Checklisten als Messinstrument:** Erfolgskriterien K1–K6 in CONCEPT.md sind bewusst agentenprüfbar formuliert
- **Grenzen kennen:** Der Agent entscheidet nicht über Projektziele – Entscheidungen (wie die Konzept-Abgrenzungen) trifft der Mensch

## Links

- [[KI-Agent-vs-Chat]] – theoretische Abgrenzung
- [[10-Wissensbasis/Erster-Workflow-Test]] – erster Praxisdurchlauf
- [[10-Wissensbasis/Git-Grundlagen]] – Verifikationsbefehle
- [[90-Index/Wissensindex]]
