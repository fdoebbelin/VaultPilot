---
description: Kursstand übernehmen – neue Kursinhalte von GitHub holen und in den eigenen Branch mein-vault mergen, eigene Änderungen bleiben abgegrenzt
agent: build
subtask: false
---

Übernimm den aktuellen Kursstand in den persönlichen Vault des Nutzers.

**Modus:** $ARGUMENTS

- `check` = nur Inventur und Bericht, **keine Änderungen am Vault**
- `apply` = Änderungen nach expliziter Bestätigung ausführen
- ohne Argument = wie `check`, anschließend `apply` anbieten

Arbeite im Vault-Root (Konvention: `$env:VAULTPILOT`, keine hartcodierten Pfade).

## Branch-Modell (verbindlich)

| Branch | Inhalt | Regel |
|---|---|---|
| `main` | Kursstand des Kursleiters | **Spiegel von `origin/main`** – hier wird nie committet |
| `mein-vault` | eigener Stand: Notizen, Daily Notes, Häkchen | hier wird gearbeitet und committet; **wird nie gepusht** |

Es gibt nur ein Remote: `origin` = Kurs-Repository auf GitHub (nur lesen).

**Verboten in diesem Command:** `git push`, `git rebase`, `git reset --hard`, `git stash`, jede Form von `--force`, Commits auf `main`, Löschen von Branches. Konflikte werden **nie** automatisch aufgelöst.

## Vorgehen

### Phase 1 – Inventur (immer zuerst, keine Änderungen am Vault)

`git fetch` aktualisiert nur die Remote-Information (`origin/main`), keine Datei im Vault – deshalb ist es auch im Modus `check` erlaubt.

```powershell
git --version                                    # (0) Git-Version – Voraussetzung für die Konflikt-Vorschau
git fetch origin --tags
git branch --show-current                          # (1) aktueller Branch
git branch --list mein-vault                       # (2) eingerichtet?
git status --porcelain                             # (3) unversionierte Änderungen?
git rev-list --count origin/main..main             # (4) Fehlbedienung: eigene Commits auf main? Soll: 0
git log --oneline mein-vault..origin/main          # (5) Kursneuerungen, die noch fehlen
git diff --stat mein-vault...origin/main           # (6) welche Kursdateien sich ändern
git log --oneline --no-merges origin/main..mein-vault   # (7) eigene Commits (zur Abgrenzung)
git merge-tree --write-tree --name-only mein-vault origin/main   # (8) Konflikt-Vorschau
```

**Zu (0):** Ist die Git-Version kleiner als 2.38, überspringe Schritt (8) komplett und vermerke das im Bericht („Konflikt-Vorschau nicht verfügbar – Git < 2.38"). Alle übrigen Schritte funktionieren auch mit älterem Git.

**Zu (8):** Exit-Code `0` = Merge läuft konfliktfrei durch. Exit-Code `1` = Konflikte erwartet; die Zeilen nach der ersten (Tree-ID) bis zur Leerzeile sind die betroffenen Dateien.

Gib einen Bericht aus:

| Prüfpunkt | Befund | Bewertung |
|---|---|---|
| aktueller Branch | … | ✅ `mein-vault` / ⚠️ sonst |
| Branch `mein-vault` vorhanden | … | ✅ / ⚠️ Einrichtung nötig |
| Arbeitsverzeichnis | sauber / n Dateien geändert | ✅ / ⛔ erst committen |
| Commits auf `main` | 0 / n | ✅ / ⛔ Fehlbedienung |
| fehlende Kursneuerungen | n Commits | ℹ️ / ✅ aktuell |
| eigene Commits | n | ℹ️ |
| erwartete Konflikte | keine / Dateiliste | ✅ / ⚠️ |

Unter der Tabelle: die Commit-Liste aus (5) und die Dateiliste aus (6). Bei Modus `check`: hier stoppen und Bericht übergeben.

### Phase 2 – Plan + Bestätigung (nur bei `apply`)

Erst die Blocker beheben – jeweils als Vorschlag, Ausführung erst nach Bestätigung:

1. **`mein-vault` fehlt** (Ersteinrichtung): `git switch -c mein-vault` vorschlagen. Unversionierte Änderungen wandern dabei mit und werden anschließend auf `mein-vault` committet.
2. **Aktueller Branch ist `main`**, `mein-vault` existiert: `git switch mein-vault` vorschlagen. Verweigert Git den Wechsel wegen unversionierter Änderungen → **stoppen**, nichts erzwingen, Nutzer an den Kursleiter verweisen.
3. **Unversionierte Änderungen** auf `mein-vault`: `git status` zeigen, Commit vorschlagen (z. B. `Stand vor Kurs-Update`): `git add -A` + `git commit -m "…"`.
4. **Commits auf `main`** (Fehlbedienung): Rettung ohne Datenverlust vorschlagen – die versehentlichen Commits zuerst nach `mein-vault` übernehmen, dann `main` auf den Kursstand zurücksetzen:

   ```powershell
   git switch mein-vault
   git merge main -m "Versehentliche main-Commits nach mein-vault übernommen"
   git branch -f main origin/main
   ```

   `git branch -f` erst ausführen, wenn der Merge erfolgreich war (`git log --oneline -3` prüfen).

Dann den eigentlichen Update-Plan ankündigen: Anzahl der Kurs-Commits, betroffene Dateien, erwartete Konflikte. **Warte auf die explizite Bestätigung des Nutzers.**

### Phase 3 – Ausführung (nur nach Bestätigung, immer auf `mein-vault`)

```powershell
git fetch origin --tags main:main            # main vorspulen, ohne den Vault anzufassen
git merge main -m "Kursstand übernommen"     # Kursstand in mein-vault holen
```

`git fetch origin main:main` aktualisiert `main` nur, wenn das ein reiner Vorlauf ist – sonst bricht es mit `rejected (non-fast-forward)` ab. Das ist gewollt: Dann liegt eine Fehlbedienung vor → zurück zu Phase 2, Punkt 4. Es wird kein Branch-Wechsel gebraucht, Obsidian sieht die Dateien nur einmal (beim Merge) ändern.

**Bei Konflikten: stoppen.** Konfliktdateien auflisten (`git diff --name-only --diff-filter=U`) und **pro Datei** eine Entscheidung erfragen:

Wichtig hierbei: `/vault-reset` setzt Checkboxen in genau den Dateien zurück, die auch `/vault-update` am häufigsten als Konflikt meldet (`Umsetzung-Checkliste.md`, Übungsdocs in `00-Inbox/`). Ein zurückgesetztes Häkchen ist also *kein* Grund, die eigene Version zu behalten.

| Datei | Empfehlung | Befehl |
|---|---|---|
| `90-Index/Wissensindex.md` | Kursversion nehmen, danach `/vault-index` neu ausführen | `git checkout --theirs -- "<datei>"` |
| Checklisten / Übungsdocs (Checkbox-Konflikt) | Kursversion nehmen – eigene Häkchen gehen dabei verloren, darauf hinweisen; ggf. danach `/vault-reset` erneut ausführen | `git checkout --theirs -- "<datei>"` |
| eigene Notiz, vom Kurs ebenfalls geändert | eigene Version behalten | `git checkout --ours -- "<datei>"` |
| unklar | Nutzer löst in Obsidian/Editor selbst auf (Konfliktmarker `<<<<<<<` `=======` `>>>>>>>` erklären) | – |
| Nutzer will abbrechen | Zustand vor dem Merge wiederherstellen | `git merge --abort` |

Hinweis zur Richtung: Im Merge auf `mein-vault` ist `--ours` = eigener Stand, `--theirs` = Kursstand.

Nach allen Entscheidungen:

```powershell
git add -A
git diff --name-only --diff-filter=U    # Soll: leer
git commit --no-edit
```

### Phase 4 – Verifikation & Abschlussbericht

```powershell
git branch --show-current                     # Soll: mein-vault
git status                                    # Soll: working tree clean
git log --oneline mein-vault..origin/main     # Soll: leer (Kursstand vollständig übernommen)
git rev-list --count origin/main..main        # Soll: 0 (main ist sauberer Spiegel)
git log --oneline --graph -10                 # Bild: eigener Strang + Kursstrang + Merge
```

Abschlussbericht: übernommene Kurs-Commits, geänderte Kursdateien, getroffene Konfliktentscheidungen (Datei → Version), Hinweis auf nötige Folgeschritte (z. B. `/vault-index` nach Index-Konflikt, `/vault-reset` nach Checkbox-Konflikt in Checkliste/Übungsdocs).

Zum Schluss den Nutzer auffordern, die Prüfung selbst nachzuvollziehen („Vertrauen durch Verifikation"): `git status` und `git log --oneline --graph -10` eigenhändig ausführen.
