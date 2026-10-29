---
title: Git-Grundlagen für den Vault-Workflow
created: 2026-10-27
updated: 2026-10-29
tags:
  - git
  - github
  - versionierung
  - wissensmanagement
status: active
---

# Git-Grundlagen für den Vault-Workflow

## Zweck

Die Git-Befehle, die im VaultPilot-Kurs täglich gebraucht werden – kompakt und auf den Vault-Workflow bezogen. Einrichtung des Repositorys: [[10-Wissensbasis/GitHub-Repository]].

## Kernbegriffe

| Begriff | Bedeutung | Im VaultPilot |
|---|---|---|
| **Repository** | Ordner mit Versionshistorie | `$env:VAULTPILOT` |
| **Clone** | Lokale Kopie aus dem Remote ziehen, inkl. kompletter Historie | Ersteinrichtung: `git clone https://github.com/fdoebbelin/VaultPilot.git $env:VAULTPILOT` |
| **Commit** | Momentaufnahme mit Kommentar | eine Arbeitsstufe, z. B. „Leitfäden ergänzt" |
| **Branch** | Namens-Label für eine Entwicklungslinie | `main` = Kursstand, `mein-vault` = deine Arbeit |
| **Remote** | Server-Adresse des Repositorys | `origin` = Kursrepo auf GitHub – **nur lesen** |
| **Fetch** | Nur „Nachschauen": den Stand des Remotes ins lokale `.git` holen – ändert **keine** Datei im Vault | immer erlaubt, auch nur zum Nachsehen |
| **Merge** | Eine Entwicklungslinie in die eigene übernehmen | `/vault-update` merged den Kursstand in `mein-vault` |
| **Pull** | `fetch` + `merge` in einem Befehl – merkt sofort in den aktuellen Branch | **entfällt für Teilnehmer** (kein eigenes Remote) |
| **Push** | Lokale Commits hochladen | **entfällt für Teilnehmer** (keine Schreibrechte) |
| **`.gitignore`** | Liste ignorierte Dateien | z. B. `.obsidian/workspace.json` |

## Branch-Modell (verbindlich)

Deine Abgrenzung vom Kursfortschritt läuft rein lokal über zwei Branches:

| Branch | Inhalt | Regel |
|---|---|---|
| `main` | Kursstand des Kursleiters | Spiegel von `origin/main` – hier wird **nie** committet |
| `mein-vault` | Dein Stand: Notizen, Daily Notes, Häkchen | hier arbeitest du und commitest – wird **nie gepusht** |

Wichtig: `mein-vault` existiert nur auf deinem Rechner (kein Backup). Wer sichergehen will, richtet optional später ein privates eigenes Remote als zusätzliches Backup-Remote nach – das Modell bleibt davon unberührt.

Warum kein `pull`? Pull mergt sofort in den aktuellen Branch – bei Teilnehmern ohne Push-Rechte ist der klare Zweischritt „nachschauen (`fetch`) → planen → mergen" verständlicher und sicherer. Genau dieser Zweischritt ist in `/vault-update` automatisiert.

## Der Sitzungszyklus (Teilnehmer)

```powershell
cd $env:VAULTPILOT

cd $env:VAULTPILOT
opencode                                         # Sessionstart im Agenten
# im Eingabefeld: /vault-update check            # 0. Inventur: fehlt dir etwas Neues vom Kurs?
# ... im Vault arbeiten (Notizen, Obsidian) ...

git status                                # 1. Prüfen: Was wurde geändert? (vor jedem Commit lesen!)
git branch --show-current                 # 2. Soll: mein-vault – sonst stoppen und klären
git add -A                                # 3. Änderungen für den Commit vormerken
git commit -m "Kurze, präzise Beschreibung"   # 4. Momentaufnahme festhalten (auf mein-vault)
```

**Faustregel:** Kleine, häufige Commits mit aussagekräftigen Meldungen schlagen seltenen Groß-Commits – jeder Commit ist ein Wiederherstellungspunkt auf `mein-vault`.

## Kursstand holen / Abgrenzung – die wichtigsten Befehle

```powershell
git fetch origin --tags                              # Nachschauen, was es Neues gibt
git log --oneline mein-vault..origin/main            # Kursneuerungen, die dir noch fehlen
git log --oneline --no-merges origin/main..mein-vault   # nur deine eigenen Commits
git diff kurs-start mein-vault                       # alles Eigene seit Kursbeginn (Tag: kurs-start)
git log --oneline --graph --all                      # Gesamtbild der Entwicklungslinien
```

## Was git status sagt – und wie man es liest

- `Changes not staged` → geänderte Dateien, noch nicht vorgemerkt (`git add` nötig)
- `Untracked files` → neue Dateien, die Git noch nicht kennt
- `nothing to commit, working tree clean` → alles committed – idealer Zustand vor/bis zur nächsten Sitzung

## Typische Probleme – und ihre Behandlung

| Problem | Symptom | Behandlung |
|---|---|---|
| Kurs überarbeitet eine Datei, die du ebenfalls geändert hast (z. B. Checkboxen, Wissensindex) | `CONFLICT (content)` beim Merge | Nie automatisch lösen: pro Datei entscheiden (`--theirs` = Kursversion meist für Checklisten/Index, `--ours` = eigene Notiz behalten). `/vault-update apply` führt durch diese Entscheidungen. |
| Unversionierte Änderungen blockieren das Übernehmen des Kursstands | `error: … local changes would be overwritten` | Erst `git status` lesen und committen – nie `git stash` (Verlustgefahr) |
| versehentlich auf `main` committet | `rejected (non-fast-forward)` | `/vault-update apply` erkennt das und rettet ohne Datenverlust (Commits nach `mein-vault`, dann `main` zurück auf den Kursstand) |
| Dich nervt dein „verbrauchter" Vault | Übungen doppelt durchlaufen? | Frischer Durchlauf ab Tag: `git switch -c versuch-2 kurs-start` |
| Mein Vault ist weg/Wiederherbarkeit | Crash, versehentliches Löschen | Nur-Lese-Remote: kein Backup für `mein-vault` – deshalb: kleine, regelmäßige Commits (jeder Commit ist ein Wiederherstellungspunkt) |

## Warum eine `.gitignore`?

Nicht alles gehört in die Versionshistorie. Das Projekt ignoriert arbeitsplatzbezogene Obsidian-Dateien (`.obsidian/workspace.json`, Cache, Papierkorb), weil sie sich bei jeder Nutzung ändern und nichts mit dem **Wissen** zu tun haben. Geteilte Konfiguration (Theme, Plugins) bleibt dagegen versioniert. Details: [[90-Index/Sitzungen/2026-10-27 Git-Ignore-Arbeitsplatzkonfiguration]].

## Kritische Prüfung (Agenten-Ausgaben verifizieren)

Wenn der Agent behauptet, „Kursstand ist übernommen" oder „alles ist committed":

1. `git status` selbst ausführen → muss `working tree clean` melden
2. `git branch --show-current` → muss `mein-vault` zeigen
3. `git log --oneline mein-vault..origin/main` → muss leer sein (Kursstand vollständig übernommen)
4. `git log --oneline --graph -10` → eigener Strang + Kursstrang + Merge sichtbar?

## Links

- [[Einstieg]] – Teilnehmer-Einstieg inkl. `/vault-update` und `/vault-reset`
- [[10-Wissensbasis/GitHub-Repository]] – Der Kurs-Klon: woher und wie
- [[10-Wissensbasis/Agenten-Workflow]] – Sitzungsablauf
- [[10-Wissensbasis/Obsidian-Grundlagen]] – Abschnitt „Arbeiten im Git-versionierten Vault"
- [[90-Index/Wissensindex]]
