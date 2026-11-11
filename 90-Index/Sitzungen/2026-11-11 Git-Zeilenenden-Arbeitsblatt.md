---
title: Sessionprotokoll Git-Zeilenenden-Arbeitsblatt
created: 2026-11-11
type: sessionprotokoll
source: opencode
model: opencode/big-pickle
tags:
  - sessionprotokoll
  - git
  - zeilenenden
  - arbeitsblatt
  - wissensbasis
status: active
---

# Sessionprotokoll – 2026-11-11 Git-Zeilenenden-Arbeitsblatt

## Ausgangslage

- **Datum:** 2026-11-11
- **Aktives OpenCode-Modell:** `opencode/big-pickle`
- **Letzter Commit (Sitzungsbeginn):** `8a1d3cd` (Merge Pull Request #1, Arbeitsbaum sauber)
- **Ziel der Sitzung:** Widersprüchliches Git-Signal erklären (`git status` meldet zwei geänderte Dateien, `git diff` zeigt nichts), beheben und als Arbeitsblatt für die Wissensbasis aufbereiten.

## Analyse

Der Arbeitsbaum war inhaltlich identisch mit dem Index, aber der **Stat-Cache** des Index war veraltet:

| Datei | Größe im Index-Stat | echte Dateigröße | Blob-Größe |
|---|---|---|---|
| `README.md` | 2719 | 2663 | 2663 |
| `10-Wissensbasis/Phase-A-Installation.md` | 1777 | 1709 | 1709 |

Beide Dateien enthielten LF; die Differenz entsprach genau einem Byte pro Zeile (56 bzw. 68). Die Blobs im Repo enthielten bereits LF – der normalisierte Inhalt war also gleich.

Historische Einordnung: Commit `cb96d70` (2026-11-10, „Zeilenenden auf LF vereinheitlichen") hat **nur** `.gitattributes` mit `* text=auto eol=lf` ergänzt; die Blobs von `README.md` waren davor und danach identisch. Die Dateien waren zuvor mit `core.autocrlf=true` als CRLF ausgecheckt worden und blieben beim Pull unangetastet (der Commit änderte sie nicht). Erst ein späterer Editor-/Formatter-Lauf schrieb sie auf LF – zurück blieb die veraltete Größe im Stat-Cache.

**Merksatz:** `git status` prüft Metadaten (Stat-Cache), `git diff` prüft den normalisierten Inhalt. Bei abweichender Größe meldet die Statusprüfung „modified", ohne den Inhalt zu vergleichen.

## Was getan wurde

### 1. Diagnose

- `git hash-object <datei>` mit `git rev-parse :<datei>` verglichen → identische Hashes (Inhalt gleich)
- `git ls-files --debug` (gemerkte Arbeitsdatei-Größe) mit `Get-Item` (echte Größe) verglichen → Größenabweichung
- `git update-index --really-refresh` getestet → meldet nur „needs update", Exit 1; keine Bereinigung
- `git diff` und `git diff-files --quiet` gegenübergestellt → leerer Diff, aber Diff-Status „modified"

### 2. Behebung

- `git add README.md "10-Wissensbasis/Phase-A-Installation.md"` → Stat-Cache aufgefrischt, nichts gestaged (Inhalt identisch); `git status --short` danach leer
- `git config --global core.autocrlf false` gesetzt (konsistent zu `eol=lf` in `.gitattributes`)
- `git add --renormalize .` ausgeführt → keine Änderungen zu stagen

### 3. Arbeitsblatt erstellt und integriert

- Erste Fassung in `00-Inbox/Arbeitsblatt Git-Zeilenenden.md` erstellt, im [[90-Index/Wissensindex]] unter „Übungen & Beispiele" verlinkt
- Nach Review nach `10-Wissensbasis/` verschoben, `status: active`; Commit `7bc62e0`

### 4. Review der überarbeiteten Fassung

Nutzer lieferte eine überarbeitete Variante mit eigenem Übungs-Repo. Die Kernaussagen wurden in einem Temp-Repo empirisch nachgestellt:

- `git status --short` → ` M README.md`; `git diff` → nur die CRLF-Warnung, kein Textunterschied
- `git ls-files --eol` → `i/lf w/crlf attr/text=auto eol=lf`
- `git hash-object README.md` == `git rev-parse :README.md`
- Index-Stat `size: 15`, echte Datei 18 Bytes
- `git update-index --refresh` → `README.md: needs update`
- `git add README.md` → Warnung erneut, danach `git diff --cached --stat` und `git status --short` leer

Review-Feststellungen (vier Korrekturen): Labor-Ort ins Temp-Verzeichnis (sonst verschachteltes Repo im Vault), „Index-Größe" als gemerkte Arbeitsdatei-Größe präzisieren, Pull-Aussage auf „dieser Commit ändert nur `.gitattributes`" eingrenzen, Übernahme-Hinweis/Status konsistent halten.

### 5. Übernahme

- Überarbeitete Fassung (v3) ersetzte die bestehende Wissensnotiz; `status: active`, Übernahme-Hinweis entfernt
- Keine Verweise auf den alten Inbox-Pfad vorhanden; Wissensindex-Eintrag blieb gültig
- Commit `9fe653a`, Push nach `origin/main` (`7bc62e0..9fe653a`)

## Probleme & Lösungen

### „modified", aber `git diff` ist leer

**Symptom:** `git status` listet zwei geänderte Dateien, `git diff` gibt nichts aus.

**Ursache:** Veralteter Stat-Cache im Index (Größe 2719/1777 statt 2663/1709); Inhalt nach Zeilenenden-Normalisierung identisch.

**Lösung:** `git add <datei>` für genau die betroffenen Dateien; danach Status prüfen.

**Verworfene Ansätze:** `git add -A` (unnötiges Risiko, ungeprüfte Änderungen zu stagen); `git checkout -- <datei>` (hätte die Dateien neu geschrieben, obwohl inhaltlich nichts fehlte).

**Verifikation:** `git hash-object <datei>` == `git rev-parse :<datei>`; `git status --short` leer; `git diff --cached` leer.

### `git update-index --refresh` bereinigt nicht

**Symptom:** `README.md: needs update`, Exit 1, Status bleibt „modified".

**Ursache:** Die Refresh-Prüfung vertraut der abweichenden Größe und hasht den Inhalt nicht neu.

**Lösung:** `git add <datei>` (aktualisiert den Stat-Cache); `git update-index --refresh` ist hier kein Ersatz.

**Verifikation:** Anschließend `git status --short` leer.

### `git add --renormalize .` falsch eingeordnet

**Symptom:** Unklarheit, ob `--renormalize` der Standard-Fix für „modified ohne Diff" ist.

**Ursache:** Der Befehl ist für geänderte/neue `.gitattributes` gedacht, nicht für einen veralteten Stat-Cache.

**Lösung:** Im konkreten Fall `git add <datei>`. `--renormalize` kann echte Blob-Änderungen stagen – Ergebnis immer mit `git diff --cached --stat` prüfen.

**Verifikation:** `git add --renormalize .` im Kurs-Repo → keine gestagten Änderungen.

### Übungs-Repo wäre im Vault gelandet

**Symptom:** Die Labor-Befehle legten `zeilenenden-labor` im aktuellen Verzeichnis an – aus dem Vault heraus ein verschachteltes Repo.

**Ursache:** Relative Pfadangabe ohne vorherigen Verzeichniswechsel.

**Lösung:** Im Arbeitsblatt v3 `Set-Location $env:TEMP` vor `git init`; Aufräumen ebenfalls von `$env:TEMP` aus.

**Verifikation:** Testlauf im Temp-Verzeichnis; Kurs-Vault blieb unberührt.

## Artefakte (neu / geändert)

- [[10-Wissensbasis/Arbeitsblatt Git-Zeilenenden]] – überarbeitetes Arbeitsblatt (Übungs-Repo, Diagnose, Fix, Vorbeugung), ersetzt die erste Fassung
- [[90-Index/Wissensindex]] – Eintrag unter „Übungen & Beispiele", `updated: 2026-11-11`
- Commit `7bc62e0` – Arbeitsblatt erstmals ergänzt und verlinkt
- Commit `9fe653a` – überarbeitete Fassung übernommen
- Maschinenlokale Konfiguration: `core.autocrlf=false` (global, kein Repo-Artefakt)

## Entscheidungen

- **Stat-Cache-Fix statt Renormalisierung** – Inhalt war identisch; `git add` ist der kleinste Eingriff.
- **`core.autocrlf=false` global** – konsistent zur Repo-Regel `* text=auto eol=lf`; vermeidet CRLF-Checkouts in Repos ohne Attribute.
- **Ersetzen statt Parallelversion** – die überarbeitete Fassung ist inhaltlich überlegen; gleicher Pfad hält den Wissensindex stabil.
- **Arbeitsblatt als Wissensnotiz** (`status: active`) – kein reines Übungsblatt in der Inbox, sondern dauerhaft nachschlagbar.

## Nützliche Befehle & Snippets

```powershell
# Inhalt vergleichen (Worktree vs. Index)
git hash-object README.md
git rev-parse :README.md

# Zeilenenden und Regel anzeigen
git ls-files --eol README.md

# Gemerkte Arbeitsdatei-Größe vs. echte Größe
git ls-files --debug README.md
(Get-Item README.md).Length

# Stat-Cache auffrischen (nur betroffene Dateien)
git add README.md

# Ergebnis prüfen
git diff --cached --stat
git status --short

# Vorbeugung
git config --global core.autocrlf false
```

## Nächste Schritte (Pickup für nächste Sitzung)

- [x] Ursache des Widerspruchs aufklären und beheben
- [x] Arbeitsblatt erstellen, reviewen und in die Wissensbasis übernehmen
- [x] Commit und Push nach `origin/main`
- [ ] Optional: In [[10-Wissensbasis/Git-Grundlagen]], Abschnitt „Typische Probleme", auf das neue Arbeitsblatt verweisen
- [ ] Pilotbegleitung: beobachten, ob Zeilenenden-Probleme bei Teilnehmern erneut auftreten (dann Feedback in die Kurs-Iteration)

---

## Handoff (für Übergabe an nächste Sitzung)

**Zusammenfassung in 1–2 Sätzen:**

Das Phantom-„modified" (Stat-Cache vs. Inhalt, CRLF/LF) ist aufgeklärt und behoben; die Erkenntnisse stehen als überarbeitetes, empirisch geprüftes Arbeitsblatt in der Wissensbasis. Die überarbeitete Fassung ersetzt die erste Version und ist gepusht (`9fe653a`).

**Wichtigste Dateien/Commits:**

- [[10-Wissensbasis/Arbeitsblatt Git-Zeilenenden]]
- Commits `7bc62e0` (Erstfassung) und `9fe653a` (überarbeitete Fassung)

**Modell:** `opencode/big-pickle`

**Offen für nächste Sitzung:**

- [ ] Optionaler Querverweis aus [[10-Wissensbasis/Git-Grundlagen]] auf das Arbeitsblatt
- [ ] Pilot-Feedback zu Zeilenenden/Git-Signalen beobachten
