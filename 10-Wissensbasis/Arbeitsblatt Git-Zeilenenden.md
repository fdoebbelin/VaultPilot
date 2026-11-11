---
title: Arbeitsblatt Git-Zeilenenden
tags: [arbeitsblatt, uebung, git, zeilenenden, aktion]
created: 2026-11-11
updated: 2026-11-11
status: active
---

# Arbeitsblatt: „modified", aber `git diff` ist leer

Praxisfall zu [[10-Wissensbasis/Git-Grundlagen]]. Dauer: ca. 10 Minuten. Am Ende kannst du das widersprüchliche Git-Signal erklären, die Ursache eingrenzen und den Stat-Cache sauber zurücksetzen.

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

Zwei Meldungen, die sich scheinbar widersprechen. Beide sind technisch korrekt – sie prüfen unterschiedliche Dinge.

## Warum das passiert: Stat-Cache vs. Inhalt

| Prüfung | Was Git vergleicht | Ergebnis |
|---|---|---|
| `git status` / `git diff-files` | Metadaten aus dem **Stat-Cache** des Index: Größe, mtime, Dateimodus | „modified" (Metadaten passen nicht) |
| `git diff` | **Inhalt** nach Zeilenenden-Normalisierung (Blob-Hash) | „keine Änderung" (Inhalt identisch) |

Der Index merkt sich bei jedem Checkout die Dateigröße. Wird eine Datei später neu geschrieben – z. B. von einem Editor oder Formatter, der die Zeilenenden vereinheitlicht –, ändert sich die Größe, der Inhalt aber nicht. `git status` sieht die abweichende Größe und behauptet „modified", bis der Cache aufgefrischt wird.

## Ursache im konkreten Fall: CRLF ↔ LF

In `.gitattributes` steht `* text=auto eol=lf`, global war aber `core.autocrlf=true` aktiv. Ablauf:

1. Checkout mit CRLF → Worktree-Datei 2719 Bytes (`README.md`) bzw. 1777 Bytes (Markdown-Notiz).
2. Später schreibt ein Werkzeug die Dateien mit LF → 2663 / 1709 Bytes.
3. Der Blob im Repo enthält bereits LF – der **normalisierte Inhalt ist also gleich**.
4. Nur die im Index gespeicherte Größe ist veraltet → `git status` meldet „modified", `git diff` schweigt.

Die Differenz war genau die Anzahl der Zeilen (56 bzw. 68 Bytes = ein Byte pro CRLF → LF).

## Diagnose in 4 Schritten

```powershell
# 1. Was behauptet Git?
git status --short

# 2. Was ist inhaltlich wirklich anders?
git diff
git diff --cached

# 3. Inhalts-Hashes vergleichen (Worktree vs. Index)
git hash-object --path=README.md README.md
git rev-parse :README.md
# gleich = Inhalt identisch, nur Metadaten veraltet

# 4. Größen vergleichen (Index-Stat vs. echte Datei)
git ls-files --debug README.md
Get-Item README.md | Select-Object Length
```

Zusatzcheck, ob die Datei noch CRLF enthält:

```powershell
$b = [IO.File]::ReadAllBytes("README.md")
$crlf = 0
for ($i = 0; $i -lt $b.Length - 1; $i++) {
    if ($b[$i] -eq 13 -and $b[$i + 1] -eq 10) { $crlf++ }
}
"CRLF: $crlf"    # 0 = reine LF-Datei
```

## Lösung

```powershell
# Variante A (empfohlen): Stat-Cache auffrischen, Inhalt bleibt unangetastet
git add README.md "10-Wissensbasis/Phase-A-Installation.md"

# Variante B: alle Dateien im Repo neu normalisieren
git add --renormalize .

# Danach immer prüfen – es darf nichts gestaged sein:
git diff --cached --stat
git status --short
```

> **Wichtig:** `git add` staged hier **nichts**, weil der Inhalt identisch ist – es aktualisiert nur den Stat-Cache. Bei echten inhaltlichen Änderungen würde derselbe Befehl sie natürlich stagen. Deshalb vorher `git diff` lesen.

## Vorbeugung

```powershell
# Passt zur Regel "* text=auto eol=lf" in .gitattributes:
git config --global core.autocrlf false
```

Wenn Attribute nachträglich geändert werden, einmalig neu normalisieren:

```powershell
git add --renormalize .
git status --short     # prüfen, dann committen
```

## Ablauf zum Selbermachen

- [ ] `git status` und `git diff` hintereinander ausführen und den Widerspruch notieren
- [ ] Für eine betroffene Datei `git hash-object --path=<datei> <datei>` mit `git rev-parse :<datei>` vergleichen
- [ ] Index-Stat-Größe (`git ls-files --debug`) mit echter Dateigröße (`Get-Item`) vergleichen
- [ ] `git add <datei>` ausführen
- [ ] `git diff --cached --stat` → muss leer sein
- [ ] `git status --short` → muss leer sein
- [ ] `git config --global core.autocrlf` → muss `false` zeigen

## Verifikation

- [ ] Du kannst in einem Satz erklären, warum `git status` und `git diff` unterschiedliche Dinge prüfen
- [ ] `git status --short` ist leer (Working Tree sauber)
- [ ] `git diff --cached` ist leer (nichts versehentlich gestaged)
- [ ] `core.autocrlf` ist global auf `false` gesetzt
- [ ] `.gitattributes` enthält weiterhin `* text=auto eol=lf`

## Andere Ursachen für „modified ohne Diff"

| Beobachtung | Wahrscheinliche Ursache | Prüfung / Behandlung |
|---|---|---|
| Größe weicht ab, Inhalt gleich | Zeilenenden (CRLF/LF), Stat-Cache | `git add <datei>` / `git add --renormalize .` |
| `old mode 100644` / `new mode 100755` | Dateirechte | `git config core.filemode false` (Windows) |
| Datei taucht doppelt mit anderer Schreibweise auf | Groß-/Kleinschreibung | `git config core.ignorecase`; Datei mit `git mv` umbenennen |
| „Binary files differ" bei Textdatei | NUL-Bytes, UTF-16, BOM | Encoding prüfen, Datei als UTF-8 speichern |
| `git diff` zeigt nur `^M`-Zeilen | gemischte Zeilenenden | `git diff --ignore-cr-at-eol` zur Kontrolle |

## Merksatz

> `git status` prüft Metadaten, `git diff` prüft Inhalt. Erst beide lesen, dann handeln – und niemals blind `git add -A` ausführen.

## Links

- [[10-Wissensbasis/Git-Grundlagen]] – Grundlagen, `git status` lesen, typische Probleme
- [[10-Wissensbasis/GitHub-Repository]] – Klon und Rollenmodell
- [[90-Index/Wissensindex]] – Einstieg in die Wissensbasis

---

**Hinweis:** Dieses Arbeitsblatt gehört zur Wissensbasis ([[90-Index/Wissensindex]]) und wird aktualisiert, wenn sich Git-Konfiguration oder `.gitattributes` ändern.
