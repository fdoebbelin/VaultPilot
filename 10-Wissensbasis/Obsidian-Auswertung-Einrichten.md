---
title: Obsidian als Auswertungsfläche einrichten
created: 2026-10-26
updated: 2026-10-26
tags:
  - obsidian
  - auswertung
  - wissensbasis
  - moc
status: active
---

# Obsidian als Auswertungsfläche einrichten

## Zweck

Obsidian als zentrale Oberfläche nutzen, um die Wissensbasis zu durchsuchen, zu verwalten und auszuwerten (Teilziel 4 aus CONCEPT.md).

## Voraussetzungen

- Obsidian installiert (Desktop-App)
- VaultPilot-Repository lokal vorhanden: `C:\Users\fritz\Projects\VaultPilot`

## Schritte

### 1. Vault in Obsidian öffnen

1. Obsidian starten
2. „Öffnen als Vault" → `C:\Users\fritz\Projects\VaultPilot` auswählen
3. Bestätigen, dass `.obsidian/`, `00-Inbox/`, `10-Wissensbasis/`, `90-Index/` sichtbar sind

### 2. Core-Plugins prüfen und aktivieren

Im Vault liegen bereits Konfigurationen in `.obsidian/`:
- `app.json` → aktivierte Core-Plugins: `daily-notes`, `templates`, `backlinks`
- `daily-notes.json` → neue Daily Notes werden in `00-Inbox/` abgelegt

In Obsidian prüfen:

1. Einstellungen (Zahnrad-Symbol) → Core Plugins
2. Folgende Plugins aktivieren (falls nicht bereits aktiv):
   - **Daily Notes**
   - **Templates**
   - **Backlinks**
   - (optional) **Starred**, **Outline**, **Page Preview**

3. Bei **Daily Notes** → „Speicherort für neue Daily Notes" auf `00-Inbox` setzen
4. Bei **Templates** → „Template-Ordner" auf z. B. `00-Inbox` oder einen eigenen `Templates`-Ordner setzen

### 3. Erste Daily Note erstellen

1. Strg+P (Befehlspalette) → „Tagesnotiz erstellen" oder über das Kalender-Symbol in der Seitenleiste
2. Die neue Notiz wird automatisch in `00-Inbox/` angelegt
3. Inhalt ergänzen und mit `[[Wikilinks]]` zu bestehenden Notizen verlinken (z. B. `[[Erster-Workflow-Test]]`, `[[VaultPilot – Konzept]]`)

### 4. Wissensindex / MOC pflegen

Im Ordner `90-Index/` können Map-of-Content (MOC)-Notizen erstellt werden, die thematisch verwandte Notizen aus `10-Wissensbasis/` sammeln und verlinken.

Beispiel-Vorgehen:
1. Neue Notiz in `90-Index/` erstellen (z. B. `90-Index/KI-Agenten.md`)
2. `[[Wikilinks]]` zu allen relevanten Notizen aus `10-Wissensbasis/` einfügen
3. Bei neuen Notizen den Index ergänzen

### 5. Backlinks nutzen

1. Eine Notiz öffnen (z. B. `10-Wissensbasis/Erster-Workflow-Test.md`)
2. In der Seitenleiste „Backlinks" anzeigen
3. Siehe, welche anderen Notizen auf diese Notiz verweisen – das zeigt das Wissensnetzwerk

## Verifikation

Nach erfolgreichem Abschluss:
- VaultPilot-Vault ist in Obsidian geöffnet
- Core-Plugins Daily Notes, Templates, Backlinks sind aktiv
- Daily Notes landen in `00-Inbox/`
- Mindestens eine Daily Note existiert und ist per `[[Wikilink]]` mit einer Wissensnotiz verknüpft
- Backlinks zeigen Verknüpfungen zwischen Notizen an

## Links

- [[90-Index/Entwicklungsprotokoll]]
- [[10-Wissensbasis/Umsetzung-Checkliste]]
- [[VaultPilot – Konzept]]
