---
title: Übungsblatt Neue Notiz
tags: [uebung, obsidian, frontmatter, aktion]
created: 2026-10-27
updated: 2026-10-27
---

# Übungsblatt: Neue Notiz anlegen

Konkrete Werte für die Layout-Übung aus [[00-Inbox/Übung Obsidian-Grundlagen]]. Das fertige Ergebnis sieht so aus wie die Muster-Notiz: [[10-Wissensbasis/Beispielnotiz-Zettelkasten|Beispielnotiz „Zettelkasten"]] – Struktur und Frontmatter identisch, **Inhalt in deinen Worten**.

## Konkrete Werte

| Feld | Wert |
|---|---|
| Notizname (Dateiname) | `Was ist ein LLM` |
| Entstehungsort | `00-Inbox/` (automatisch, siehe Standardordner) |
| Template | `Wissensnotiz` |
| `tags` | `ki-grundlagen`, `llm` |
| `created` / `updated` | heute – die Platzhalter `{{date:YYYY-MM-DD}}` füllen sich beim Template-Einfügen automatisch |
| `status` | Vorlage setzt `draft` → nach der Ausarbeitung auf `active` ändern |
| Zielsortierort | `10-Wissensbasis/` (per Drag & Drop im Datei-Explorer verschieben) |

## Schritte

1. `Strg+O` (Quick Switcher) → `Was ist ein LLM` tippen → da es die Notiz noch nicht gibt, mit `Enter` anlegen – sie entsteht in `00-Inbox/` (Alternative: `Strg+N` und danach über Rechtsklick auf den Tab-Reiter umbenennen)
2. `Strg+P` → „Vorlage" tippen → „Vorlage einfügen" → `Wissensnotiz` wählen → Frontmatter und Grundstruktur erscheinen mit `{{title}}` = `Was ist ein LLM`
3. Frontmatter anpassen: `tags: [ki-grundlagen, llm]`
4. Inhalt in **eigenen Worten** ausformulieren (2–3 Stichpunkte genügen): Was macht ein LLM? Was bedeutet „trainiert"? Wie hängt das mit [[KI-Agent-vs-Chat]] zusammen? – nicht kopieren, das ist das Zettelkasten-Prinzip (siehe Muster-Notiz)
5. Mindestens **zwei Wikilinks** setzen, aus der Autocomplete-Liste wählen – vorgesehene Ziele: [[KI-Agent-vs-Chat]] und [[10-Wissensbasis/Obsidian-Grundlagen]] (beide existieren bereits; **keine** erfundenen Namen, sonst entstehen Stub-Notizen in der Wurzel!)
6. Im [[90-Index/Wissensindex]] unter „Übungen & Beispiele" eine Zeile ergänzen: `- [[Was ist ein LLM]]`
7. Notiz per Drag & Drop nach `10-Wissensbasis/` verschieben; `status` auf `active` setzen
8. (Optional) In OpenCode `/vault-link "Was ist ein LLM"` ausführen – der Agent ergänzt weitere passende Verweise; danach verifizieren

## Verifikation

- [ ] Notiz heißt genau `Was ist ein LLM` und liegt in `10-Wissensbasis/`
- [ ] Frontmatter vollständig: `title`, `tags`, `created`, `updated`, `status`
- [ ] Mindestens 2 Wikilinks, alle klicken auf existierende Notizen (Wurzel prüfen: keine Stub-Notizen entstanden)
- [ ] Eintrag im [[90-Index/Wissensindex]] vorhanden
- [ ] `git status` zeigt die neue Datei → `git add` → `git commit` → `git push` (siehe [[10-Wissensbasis/Git-Grundlagen]])

## Links

- [[10-Wissensbasis/Beispielnotiz-Zettelkasten]] – das Muster (Zielfoto)
- [[00-Inbox/Übung Obsidian-Grundlagen]] – übergeordnete Übungsliste
- [[90-Index/Templates/Wissensnotiz]] – die verwendete Vorlage
