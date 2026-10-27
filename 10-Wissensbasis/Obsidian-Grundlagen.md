---
title: Obsidian Grundlagen
created: 2026-10-27
updated: 2026-10-27
tags:
  - obsidian
  - grundlagen
  - markdown
  - wikilinks
  - bedienung
status: active
---

# Obsidian Grundlagen

## Zweck

Einführung in die Bedienung von Obsidian für die VaultPilot-Teilnehmer: Oberfläche, Markdown-Editing, Verlinkung, Suche und Auswertung (Ergänzung zu Phase C, Teilziel 4 aus CONCEPT.md).

Installation und Vault-Setup: [[10-Wissensbasis/Obsidian-Installation-Einrichtung]].

## Kernidee: Notizen als Dateien + Links als Netzwerk

- Jede Notiz ist eine **Markdown-Datei** (`.md`) im Vault-Ordner – auch ohne Obsidian lesbar und per Git versionierbar
- Verknüpfungen entstehen über **Wikilinks** `[[Notizname]]` – Obsidian baut daraus automatisch Backlinks und einen Graphen
- Der Wert einer Wissensbasis wächst durch **Verlinkung**, nicht durch Ordnerhierarchie – Ordner grob sortieren (wie hier: `00-Inbox/`, `10-Wissensbasis/`, `90-Index/`), Feinstruktur über Links

## Oberfläche

| Element | Funktion |
|---|---|
| Linke Seitenleiste | Datei-Explorer (Ordner/Dateien), Suche, Bookmarks |
| Rechte Seitenleiste | Backlinks, Outline, Tags |
| Hauptbereich | Tabs; per Rechtsklick → „Split" in mehrere Panes teilbar |
| Statusleiste unten | Wortanzahl, Backlink-/Linkanzahl der offenen Notiz |
| Tab-Stammbaum | Oben am Tab: Pfeile für Navigationshistorie (vor/zurück) |

## Die wichtigsten Tastenkürzel

| Kürzel | Funktion |
|---|---|
| `Strg+P` | Befehlspalette (alle Befehle, inkl. Plugins) |
| `Strg+O` | Quick Switcher (Notiz schnell öffnen, by name) |
| `Strg+Shift+F` | Globale Suche über alle Notizen |
| `Strg+N` | Neue Notiz |
| `Strg+E` | Umschalten Lesen/Editieransicht |
| `Strg+K` | Link einfügen |
| `[[` eingeben | Wikilink-Auswahlliste (Autocomplete über alle Notizen) |
| `Strg+G` | Graph-Ansicht (Befehl „Open graph view") |

**Faustregel:** Befehlspalette (`Strg+P`) statt Menüs suchen – fast alles ist dort erreichbar und benennbar.

## Markdown-Grundlagen

```markdown
# Überschrift Ebene 1
## Überschrift Ebene 2

Text mit **Fettdruck**, *Kursivschrift* und `Code`.

- Liste
- Liste
  - Unterpunkt

1. nummerierte Liste
2. zweiter Punkt

> Blockzitat

```python
# Codeblock mit Sprachsyntax
print("Hallo")
```

| Spalte A | Spalte B |
|---|---|
| Zelle 1 | Zelle 2 |

- [ ] Aufgabe (Task-Liste)
- [x] erledigt

[[Wikilink zu anderer Notiz]]
[[Notizname|Anzeigetext]]
![[Notizname]]  <!-- Transklusion: Inhalt einbetten -->
[Externer Link](https://example.com)
```

**Frontmatter** (wie in allen VaultPilot-Notizen): YAML-Block ganz oben mit `title`, `created`, `updated`, `tags`, `status` – Obsidian zeigt Tags und Properties damit strukturiert an.

## Verlinkung & Auswertung

1. **Wikilink setzen:** `[[` tippen → Notiz auswählen oder neuen Namen eingeben (erzeugt beim Speichern eine neue Notiz)
2. **Backlinks prüfen:** Notiz öffnen → rechte Seitenleiste → „Backlinks" – zeigt, welche Notizen auf diese verweisen (das eigentliche Wissensnetzwerk)
3. **Graph öffnen:** Befehlspalette → „Open graph view" – Knoten = Notizen, Kanten = Links; lokale Graphansicht einer einzelnen Notiz über „Open local graph"
4. **MOCs pflegen:** In `90-Index/` liegen Map-of-Content-Notizen, die thematisch verlinken – Vorgehen: [[10-Wissensbasis/Obsidian-Auswertung-Einrichten]]
5. **Daily Notes:** Befehlspalette → „Tagesnotiz erstellen" – landet in `00-Inbox/` und wird mit dem Tagesdatum benannt

## Arbeiten im Git-versionierten Vault

Dieser Vault ist ein Git-Repository – Obsidian und Git arbeiten parallel auf denselben Dateien:

- **Obsidian nur lokal:** Änderungen erscheinen sofort in `git status`; Obsidian braucht dabei nicht geschlossen zu werden
- **Sync-Regel:** vor Sitzungsbeginn `git pull`, nach Sitzungsende `git add` → `git commit` → `git push` (siehe Checkliste Phase D)
- **Konflikte vermeiden:** nicht auf zwei Geräten gleichzeitig ungespeichert arbeiten; vor dem Wechsel des Geräts immer pushen/pullen
- **Arbeitsplatzbezogene Dateien** (z. B. `.obsidian/workspace.json`) sind über `.gitignore` ausgeschlossen – sie tauchen nie in `git status` auf ([[90-Index/Sitzungen/2026-10-27 Git-Ignore-Arbeitsplatzkonfiguration]])

## Übungen (Verifikation)

- [ ] Notiz per `Strg+O` (Quick Switcher) öffnen
- [ ] In einer Notiz `[[` tippen und einen Link auf eine bestehende Notiz setzen
- [ ] Backlinks-Pane öffnen und die Verknüpfung beide Richtungen prüfen
- [ ] Notiz teilen: Rechtsklick auf Tab → „Split right" – zwei Notizen nebeneinander
- [ ] Globale Suche (`Strg+Shift+F`) nach einem Begriff aus der Wissensbasis
- [ ] Graph-Ansicht öffnen und die Verlinkungsstruktur betrachten
- [ ] Neue Notiz mit Frontmatter anlegen und in einen MOC verlinken (z. B. über `/vault-index`)

## Links

- [[10-Wissensbasis/Obsidian-Installation-Einrichtung]] – Installation & Vault-Setup
- [[10-Wissensbasis/Obsidian-Auswertung-Einrichten]] – Auswertungs-Setup (Phase C)
- [[90-Index/Entwicklungsprotokoll]]
- [[10-Wissensbasis/Umsetzung-Checkliste]]
