---
title: Arbeitsblatt Git-Zeilenenden
tags: [arbeitsblatt, uebung, git, zeilenenden, aktion]
created: 2026-11-11
updated: 2026-11-11
status: active
---

# Arbeitsblatt: „modified", aber `git diff` ist leer

Praxisfall zu [[10-Wissensbasis/Git-Grundlagen]]. Dauer: ca. 20 Minuten. Du stellst das widersprüchliche Git-Signal in einem Übungs-Repo selbst her, grenzt die Ursache ein und behebst es.

## Lernziel

Du kannst beantworten: **Warum meldet `git status` Änderungen, obwohl `git diff` nichts zeigt – und was ist die richtige Reaktion?**

## Das Symptom

```powershell
git diff        # (keine Ausgabe)
git status
# Changes not staged for commit:
#         modified:   10-Wissensbasis/Phase-A-Installation.md
#         modified:   README.md
```

Zwei Meldungen, die sich scheinbar widersprechen. Beide sind technisch korrekt.

## Warum das passiert

Git merkt sich im Index zu jeder Datei Metadaten, unter anderem die **Dateigröße** und die Änderungszeit (Stat-Cache). Damit muss es nicht bei jedem `git status` alle Dateien neu lesen.

| Situation | Was Git tut | Ergebnis |
|---|---|---|
| Größe und Zeit unverändert | nichts, Datei gilt als unverändert | sauber |
| nur die Änderungszeit ist anders | liest den Inhalt und vergleicht | sauber, wenn der Inhalt gleich ist |
| die **Größe** ist anders | meldet „modified", **ohne** den Inhalt zu vergleichen | „modified" |

`git diff` vergleicht dagegen den Inhalt, bei Textdateien nach der Zeilenenden-Normalisierung (Binärdateien werden nicht normalisiert). Behandelt Git eine Datei als Text (hier durch `text=auto`), sind die Fassung mit CRLF und die Fassung mit LF für `git diff` deshalb gleich, aber unterschiedlich groß. `eol=lf` legt zusätzlich fest, mit welchen Zeilenenden Git die Datei auscheckt. Genau dann entsteht der Widerspruch.

## Der Praxisfall: CRLF ↔ LF

Im Repo steht `* text=auto eol=lf` in `.gitattributes`. Auf dem Rechner war global `core.autocrlf=true` gesetzt.

Wichtig: Sobald die Regel `eol=lf` für eine Datei gilt, hat sie Vorrang vor `core.autocrlf`. Ein Checkout liefert dann LF. Die CRLF-Dateien können also nur entstanden sein, **bevor** die Regel galt. Der wahrscheinliche Ablauf:

1. Checkout zu einem Zeitpunkt, als `.gitattributes` noch nicht im Repo war → `core.autocrlf=true` greift, die Dateien landen mit CRLF im Arbeitsverzeichnis: 2719 Bytes (`README.md`) bzw. 1777 Bytes (Markdown-Notiz).
2. `.gitattributes` kommt per `git pull` dazu. Dieser Commit ändert nur `.gitattributes` – die vorhandenen Dateien fasst Git deshalb nicht an, sie behalten CRLF.
3. Später schreibt ein Werkzeug (Editor, Formatter) die Dateien mit LF → 2663 / 1709 Bytes.
4. Der Inhalt im Repo hat ohnehin LF, der normalisierte Inhalt ist gleich. Nur die im Index gemerkte Größe der Arbeitsdatei ist veraltet → `git status` meldet „modified", `git diff` schweigt.

Die Differenz ist genau ein Byte pro Zeile: 56 bzw. 68 Bytes.

## Übung: das Phantom selbst erzeugen

Arbeite in einem Wegwerf-Repo im Temp-Verzeichnis, nicht in deinem Kurs-Vault. Der erste Befehl wechselt dorthin, damit kein verschachteltes Repo im Vault entsteht.

### 1. Übungs-Repo anlegen

```powershell
Set-Location $env:TEMP
git init zeilenenden-labor
Set-Location zeilenenden-labor

[IO.File]::WriteAllText((Join-Path $PWD ".gitattributes"), "* text=auto eol=lf`n")
[IO.File]::WriteAllText((Join-Path $PWD "README.md"), "eins`nzwei`ndrei`n")

git add .
git commit -m "Start"
git status --short      # leer
```

`Join-Path $PWD` ist nötig, weil `[IO.File]` relative Pfade nicht immer vom aktuellen PowerShell-Verzeichnis aus auflöst.

### 2. Datei mit anderen Zeilenenden neu schreiben

Derselbe Text, diesmal mit CRLF – so, wie es ein Editor unbemerkt tun kann:

```powershell
[IO.File]::WriteAllText((Join-Path $PWD "README.md"), "eins`r`nzwei`r`ndrei`r`n")
```

### 3. Den Widerspruch ansehen

```powershell
git status --short
#  M README.md

git diff
# warning: in the working copy of 'README.md', CRLF will be replaced by LF the next time Git touches it
```

`git diff` zeigt keinen Unterschied. Die Warnung ist kein Diff, sondern ein Hinweis auf die Ursache. (Im Praxisfall oben lief es umgekehrt, von CRLF nach LF; dann erscheint keine Warnung.)

### 4. Diagnose

```powershell
# Zeilenenden im Index (i/), im Arbeitsverzeichnis (w/) und die geltende Regel
git ls-files --eol README.md
# i/lf    w/crlf  attr/text=auto eol=lf   README.md

# Inhalts-Hash der Datei und des Index-Eintrags
git hash-object README.md
git rev-parse :README.md
# zwei gleiche Hashes = Inhalt identisch

# gemerkte Größe der Arbeitsdatei beim letzten Index-Update und echte Dateigröße
git ls-files --debug README.md      # Zeile "size: 15"
(Get-Item README.md).Length         # 18
```

`size` ist die Größe, die die Arbeitsdatei hatte, als Git den Index-Eintrag zuletzt aktualisiert hat – nicht die Größe des gespeicherten Inhalts im Repo. 15 Bytes gemerkt, 18 Bytes auf der Platte: drei Zeilen, drei zusätzliche CR-Bytes. Der Inhalt ist gleich, die Größe nicht.

### 5. Beheben

```powershell
git add README.md
```

`git add` staged hier **nichts**, weil der Inhalt identisch ist. Es trägt nur die neue Größe in den Index ein. Dabei erscheint noch einmal die CRLF-Warnung aus Schritt 3 – das ist kein Fehler.

```powershell
git diff --cached --stat    # leer: nichts gestaged
git status --short          # leer: Arbeitsverzeichnis sauber
```

> **Wichtig:** Bei echten inhaltlichen Änderungen würde derselbe Befehl sie stagen. Deshalb immer zuerst `git diff` lesen und nur die betroffenen Dateien angeben.

`git update-index --refresh` hilft hier nicht, es meldet nur `README.md: needs update`.

### 6. Aufräumen

```powershell
Set-Location $env:TEMP
Remove-Item zeilenenden-labor -Recurse -Force
```

## Checkliste zur Übung

- [ ] Übungs-Repo angelegt, `git status --short` ist leer
- [ ] Datei mit CRLF neu geschrieben
- [ ] `git status --short` zeigt ` M README.md`, `git diff` zeigt keinen Unterschied
- [ ] `git ls-files --eol` zeigt `i/lf` und `w/crlf`
- [ ] Die beiden Hashes sind gleich
- [ ] Gemerkte Größe (`size`) und echte Dateigröße weichen um die Zeilenzahl ab
- [ ] Nach `git add README.md` sind `git diff --cached --stat` und `git status --short` leer

## Im echten Repo

Das Vorgehen ist dasselbe: `git diff` lesen, mit `git ls-files --eol <datei>` die Zeilenenden prüfen, dann `git add <datei>` für genau die betroffenen Dateien.

`git add --renormalize .` ist für einen anderen Fall gedacht: wenn `.gitattributes` neu eingeführt oder geändert wurde und im Repo noch Dateien mit CRLF gespeichert sind. Der Befehl kann dann echte Änderungen stagen. Ergebnis mit `git diff --cached --stat` prüfen und bewusst committen.

## Vorbeugung

- `.gitattributes` mit `* text=auto eol=lf` gehört in den ersten Commit eines Repos. Dann gilt die Regel schon beim ersten Checkout.
- Editor und Formatter auf LF einstellen.
- Optional: `git config --global core.autocrlf false`. Das verhindert CRLF-Checkouts in Repos, die keine `.gitattributes` haben. Wo `eol=lf` gilt, spielt die Einstellung keine Rolle.

## Verifikation

- [ ] Du kannst in einem Satz erklären, warum `git status` „modified" melden kann, obwohl `git diff` leer ist
- [ ] Du kannst mit `git ls-files --eol` die Zeilenenden einer Datei bestimmen
- [ ] Du weißt, warum du vor `git add` zuerst `git diff` liest
- [ ] Im Kurs-Repo zeigt `git ls-files --eol README.md` die Regel `attr/text=auto eol=lf`

## Verwandte Fälle

Hier zeigt `git diff` etwas an, aber keinen sichtbaren Textunterschied:

| `git diff` zeigt | Wahrscheinliche Ursache | Prüfung / Behandlung |
|---|---|---|
| `old mode 100644` / `new mode 100755` | Dateirechte | `git config core.filemode` prüfen (unter Windows normalerweise `false`) |
| „Binary files differ" bei einer Textdatei | NUL-Bytes, UTF-16 | Encoding prüfen, Datei als UTF-8 speichern |
| nur Zeilen mit `^M` am Ende | CRLF in einer Datei ohne Zeilenenden-Regel | `git diff --ignore-cr-at-eol` zur Kontrolle, `.gitattributes` ergänzen |

## Merksatz

> Meldet `git status` „modified" und `git diff` nichts, stimmt meist nur die gemerkte Dateigröße nicht. Erst `git diff` lesen, dann gezielt `git add <datei>` – niemals blind `git add -A`.

## Links

- [[10-Wissensbasis/Git-Grundlagen]] – Grundlagen, `git status` lesen, typische Probleme
- [[10-Wissensbasis/GitHub-Repository]] – Klon und Rollenmodell
- [[90-Index/Wissensindex]] – Einstieg in die Wissensbasis
