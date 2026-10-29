---
description: Definierter Startpunkt herstellen – 00-Inbox auf Startdokumente prüfen, Checkboxen im Arbeitsmaterial zurücksetzen
agent: build
subtask: false
---

Stelle den definierten Startpunkt des VaultPilot-Vaults her.

**Modus:** $ARGUMENTS

- `check` = nur Inventur und Bericht, **keine Änderungen**
- `apply` = Änderungen nach expliziter Bestätigung ausführen
- ohne Argument = wie `check`, anschließend `apply` anbieten

Arbeite im Vault-Root (Konvention: `$env:VAULTPILOT`, keine hartcodierten Pfade).

## Definition: definierter Startzustand

**Startdokumente in `00-Inbox/`** – dort dürfen NUR diese zwei Dateien liegen:

- `Übung Obsidian-Grundlagen.md`
- `Übungsblatt Neue Notiz.md`

Alles andere in `00-Inbox/` (Daily Notes alter Tage, Übungsergebnisse, versehentliche Stub-Notizen) ist **Überschuss**.

**Checkbox-Zurücksetzung gilt nur für Arbeitsmaterial:**

- `10-Wissensbasis/Umsetzung-Checkliste.md`
- alle `.md`-Dateien direkt in `00-Inbox/` (nach dem Aufräumen = exakt die Startdokumente)

**Ausdrücklich NICHT anfassen** (Historie/Status bleiben unverändert): `90-Index/Sitzungen/*`, alle Daily Notes, `README.md`, `CONCEPT.md`, `Abschlussbericht.md`, `90-Index/*` übrige Dateien, `10-Wissensbasis/*` übrige Notizen (inkl. vorhandener Übungsergebnisse – Reset leert nur die Kästchen, löscht keine Inhalte).

## Vorgehen

### Phase 1 – Inventur (immer zuerst, keine Änderungen)

1. Liste alle Dateien in `00-Inbox/` auf; kennzeichne: Startdokument oder Überschuss.
2. Zähle je Ziel-Datei die angehakten Checkboxen (`- [x]` / `- [X]`), z. B. per `Select-String`.
3. Gib einen tabellarischen Bericht aus: Datei | Einstufung | geplante Aktion | Anzahl `[x]`.
4. Bei Modus `check`: hier stoppen und Bericht übergeben.

### Phase 2 – Plan + Bestätigung (nur bei `apply`)

1. Für jede Überschuss-Datei einen Vorschlag unterbreiten:
   - **Wissensinhalt** (ausgearbeitete Notiz) → Verschiebung nach `10-Wissensbasis/` vorschlagen
   - **veraltet/unerwünscht** → Löschen vorschlagen
   - **unklar** → Behalten vorschlagen und nachfragen
2. Checkbox-Reset ankündigen (Dateiliste + Trefferzahlen).
3. **Warte auf die explizite Bestätigung des Nutzers.** Niemals ohne Bestätigung löschen oder verschieben (Agenten-Regel: keine Löschungen ohne explizite Nutzeranfrage).

### Phase 3 – Ausführung (nur nach Bestätigung)

1. Überschuss-Dateien wie bestätigt behandeln; jede Verschiebung mit altem → neuem Pfad im Bericht notieren.
2. Checkboxen zurücksetzen – nur in den Ziel-Dateien, z. B. per PowerShell:

   ```powershell
   $ziel = @("10-Wissensbasis\Umsetzung-Checkliste.md") + (Get-ChildItem "00-Inbox" -Filter *.md).FullName
   $ziel | ForEach-Object {
     (Get-Content $_ -Raw) -replace '- \[[xX]\]', '- [ ]' | Set-Content $_ -NoNewline
   }
   ```

   (Alternativ: Datei für Datei mit dem Edit-Werkzeug.)
3. **Kein automatischer Commit** – Änderungen liegen zunächst unversioniert vor.

### Phase 4 – Verifikation & Abschlussbericht

1. `00-Inbox/` erneut listen → muss exakt die zwei Startdokumente enthalten (plus: was der Nutzer in Phase 2 ausdrücklich behalten wollte).
2. Ziel-Dateien nach `- [x]` durchsuchen → erwartet: 0 Treffer.
3. `git status` zusammenfassen und einen Commit-Vorschlag unterbreiten (z. B. `vault-reset: definierter Startpunkt hergestellt`) – Ausführung erst nach Bestätigung.
