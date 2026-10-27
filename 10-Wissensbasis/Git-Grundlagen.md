---
title: Git-Grundlagen für den Vault-Workflow
created: 2026-10-27
updated: 2026-10-27
tags:
  - git
  - github
  - versionierung
  - wissensmanagement
status: active
---

# Git-Grundlagen für den Vault-Workflow

## Zweck

Die Git-Befehle, die im VaultPilot-Kurs täglich gebraucht werden – kompakt und auf den Vault-Workflow bezogen (Kernnotiz zu Erfolgskriterium K2). Einrichtung des Repositorys: [[10-Wissensbasis/GitHub-Repository]].

## Kernbegriffe

| Begriff | Bedeutung | Im VaultPilot |
|---|---|---|
| **Repository** | Ordner mit Versionshistorie | `$env:VAULTPILOT` |
| **Commit** | Momentaufnahme mit Kommentar | eine Arbeitsstufe, z. B. „Leitfäden ergänzt" |
| **Remote** | Server-Kopie des Repositorys | `origin` = GitHub |
| **Clone** | Lokale Kopie aus dem Remote ziehen | Ersteinrichtung auf neuem Rechner |
| **Pull** | Änderungen vom Remote holen | **vor** jeder Sitzung |
| **Push** | Lokale Commits hochladen | **nach** jeder Sitzung |
| **`.gitignore`** | Liste ignorierte Dateien | z. B. `.obsidian/workspace.json` |

## Der tägliche Zyklus

```powershell
cd $env:VAULTPILOT

git pull          # 1. Aktualisieren (vor der Arbeit – schützt vor Konflikten)
# ... im Vault arbeiten (Notizen, Obsidian) ...

git status        # 2. Prüfen: Was wurde geändert? (vor jedem Commit lesen!)
git add .         # 3. Änderungen für den Commit vormerken
git commit -m "Kurze, präzise Beschreibung"   # 4. Momentaufnahme festhalten
git push          # 5. Auf GitHub hochladen
```

**Faustregel:** Kleine, häufige Commits mit aussagekräftigen Meldungen schlagen seltenen Groß-Commits – jeder Commit ist ein Wiederherstellungspunkt.

## Was git status sagt – und wie man es liest

- `Changes not staged` → geänderte Dateien, noch nicht vorgemerkt (`git add` nötig)
- `Untracked files` → neue Dateien, die Git noch nicht kennt
- `nothing to commit, working tree clean` → alles committed und gepusht, idealer Sitzungsendzustand

## Warum eine `.gitignore`?

Nicht alles gehört in die Versionshistorie. Das Projekt ignoriert arbeitsplatzbezogene Obsidian-Dateien (`.obsidian/workspace.json`, Cache, Papierkorb), weil sie sich bei jeder Nutzung ändern und nichts mit dem **Wissen** zu tun haben. Geteilte Konfiguration (Theme, Plugins) bleibt dagegen versioniert. Details: [[90-Index/Sitzungen/2026-10-27 Git-Ignore-Arbeitsplatzkonfiguration]].

## Kritische Prüfung (Agenten-Ausgaben verifizieren)

Wenn der Agent behauptet, „alles ist committed und gepusht":

1. `git status` selbst ausführen → muss `working tree clean` melden
2. `git log --oneline -3` → eigene Commits sichtbar?
3. Auf GitHub die Repository-Seite aktualisieren → neuester Commit oben?

## Links

- [[10-Wissensbasis/GitHub-Repository]] – Einrichtung des Remote
- [[10-Wissensbasis/Agenten-Workflow]] – Sitzungsablauf mit Git
- [[10-Wissensbasis/Obsidian-Grundlagen]] – Abschnitt „Arbeiten im Git-versionierten Vault"
- [[90-Index/Wissensindex]]
