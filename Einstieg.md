---
title: VaultPilot – Einstieg
created: 2026-10-29
updated: 2026-10-29
tags:
  - einstieg
  - onboarding
  - vaultpilot
status: active
---

# VaultPilot – Einstieg für Außenstehende

Dieses Dokument ist der Eintrittspunkt in das Projekt: Was ist VaultPilot, was brauchst du, und in welcher Reihenfolge gehst du die Schritte an?

## Was ist VaultPilot?

VaultPilot ist ein Kursprojekt zur Arbeit mit **agentischer KI** am Beispiel von **OpenCode**. Im Zentrum steht der Aufbau und die Verwaltung eines **Obsidian Vaults** als Wissensbasis („zweites Gehirn"): Wissen strukturiert ablegen, vernetzen und dauerhaft pflegen – unterstützt durch einen KI-Agenten, der Notizen erstellt, vernetzt und den Vault per Git versioniert.

Besonderheit: **Der Vault ist sein eigenes Demonstrationsobjekt.** Sämtliche Projektartefakte – dieses Dokument, die Leitfäden, die Protokolle, das Konzept – sind im gezeigten Workflow vom Agenten entstanden und vom Nutzer verifiziert worden. Was du hier liest, ist zugleich das Ergebnis der Methode.

## Was du vorab brauchst

- Windows mit PowerShell (der Kurs ist Windows-basiert)
- Git und ein GitHub-Konto (Repository: <https://github.com/fdoebbelin/VaultPilot>)
- Bereitschaft, Agenten-Aussagen zu prüfen statt ihnen zu vertrauen – das ist der didaktische Kern („Vertrauen durch Verifikation")

## Dein Weg in 7 Schritten

| # | Schritt | Leitfaden |
|---|---------|-----------|
| 1 | Repository holen + Pfad-Variable `$env:VAULTPILOT` einrichten | [README – Einrichtung](README.md) |
| 2 | OpenCode installieren (PowerShell + scoop) | [Phase A – Installation](10-Wissensbasis/Phase-A-Installation.md) |
| 3 | Obsidian installieren und diesen Ordner als Vault öffnen | [Obsidian Installation & Einrichtung](10-Wissensbasis/Obsidian-Installation-Einrichtung.md) |
| 4 | Obsidian-Grundlagen lesen (Oberfläche, Markdown, Wikilinks, Graph) | [Obsidian Grundlagen](10-Wissensbasis/Obsidian-Grundlagen.md) |
| 5 | Übungen durchführen (Tastenkürzel, Split, Graph, erste eigene Notiz) | [Übung Obsidian-Grundlagen](00-Inbox/Übung%20Obsidian-Grundlagen.md) + [Übungsblatt Neue Notiz](00-Inbox/Übungsblatt%20Neue%20Notiz.md) · Muster: [Beispielnotiz Zettelkasten](10-Wissensbasis/Beispielnotiz-Zettelkasten.md) |
| 6 | Mit dem Agenten arbeiten (`/vault-new`, `/vault-link`, `/vault-index`) | [Agenten-Workflow](10-Wissensbasis/Agenten-Workflow.md) |
| 7 | Sitzungsrhythmus etablieren: `git pull` → arbeiten → `commit`/`push` | [Git-Grundlagen](10-Wissensbasis/Git-Grundlagen.md) + [Entwicklungsprotokoll](90-Index/Entwicklungsprotokoll.md) |

Die detaillierte Aufgabenliste dahinter: [Umsetzung-Checkliste](10-Wissensbasis/Umsetzung-Checkliste.md) (Phasen A–D).

## Der definierte Startpunkt: `/vault-reset`

Vor einer neuen Übungs- oder Kurssession stellt dieser OpenCode-Command einen reproduzierbaren Zustand her:

```powershell
cd $env:VAULTPILOT
opencode
# im Eingabefeld:  /vault-reset check   → nur Inventur, keine Änderungen
#                  /vault-reset apply   → Änderungen nach Bestätigung
```

Er macht genau zwei Dinge – und bewusst nichts anderes:

1. **00-Inbox prüfen:** Dort dürfen nur die zwei Startdokumente liegen (`Übung Obsidian-Grundlagen`, `Übungsblatt Neue Notiz`) – plus die Daily Note des aktuellen Tages als aktives Arbeitsmittel. Alles andere meldet der Agent als Überschuss und schlägt pro Datei einen Umgang vor: ausgearbeitete Notizen verschieben nach `10-Wissensbasis/`; **abgearbeitete Daily Notes nach `20-Archiv/` archivieren – das nimmst du selbst in Obsidian per Drag & Drop vor**, damit Obsidian die Wikilinks automatisch aktualisiert (der Agent verschiebt sie bewusst nicht per Dateisystem); unverlinktes Zeug löschen. **Nichts wird ohne deine Bestätigung verschoben oder gelöscht.**
2. **Checkboxen zurücksetzen:** Alle `- [x]` im Arbeitsmaterial (Umsetzung-Checkliste + Übungsdocs in 00-Inbox) werden zu `- [ ]`, damit Übungen erneut durchlaufen werden können.

Nicht angefasst werden Historie und Statusdokumente: Sessionprotokolle, Daily Notes, `README.md`, `CONCEPT.md`, `Abschlussbericht.md`, der Wissensindex und die übrigen Wissensnotizen.

## Landkarte: Wo finde ich was?

| Ort | Inhalt |
|---|---|
| `README.md` | Kurzüberblick, Einrichtung, Roadmap |
| `Einstieg.md` | dieses Dokument |
| `CONCEPT.md` | finalisiertes Projektkonzept (Teilziele, Abgrenzungen, Erfolgskriterien K1–K6, Meilensteine M1–M4) |
| `Abschlussbericht.md` | Projektabschluss mit Status aller Erfolgskriterien |
| `00-Inbox/` | Startdokumente (Übungen) + Daily Note des aktuellen Tages (Erfassung) |
| `20-Archiv/` | abgearbeitete Daily Notes und Aussortiertes – Archivierung in Obsidian per Drag & Drop (Wikilinks bleiben erhalten) |
| `10-Wissensbasis/` | Wissensnotizen und Leitfäden (Kernnotizen, Checkliste) |
| `90-Index/` | [Wissensindex (MOC)](90-Index/Wissensindex.md) · [Entwicklungsprotokoll](90-Index/Entwicklungsprotokoll.md) mit allen [Sessionprotokollen](90-Index/Sitzungen/) · [Vorlage für Notizen](90-Index/Templates/Wissensnotiz.md) |
| `.opencode/` | Agent-Konfiguration und Slash-Commands (`vault-new`, `vault-link`, `vault-index`, `vault-reset`) |

## Grundregel: Vertrauen durch Verifikation

Prüfe Agenten-Aussagen selbst: `git status` ausführen statt „ist gepusht" zu glauben, Dateien öffnen statt „ist erstellt" zu akzeptieren. Drei von der Nutzerwirkung gemeldete Fehlerfunde (2026-10-27) haben die Kursmaterialien messbar verbessert – Fehlerfunde sind ausdrücklich erwünscht und werden im Sessionprotokoll dokumentiert.

## Links

- [Wissensindex (MOC)](90-Index/Wissensindex.md) – Einstieg in die Wissensbasis
- [Entwicklungsprotokoll](90-Index/Entwicklungsprotokoll.md) – Sitzungshistorie und aktueller Handoff
