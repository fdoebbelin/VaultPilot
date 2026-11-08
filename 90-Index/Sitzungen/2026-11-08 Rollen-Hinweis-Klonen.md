---
title: Sessionprotokoll Rollen-Hinweis Klonen
created: 2026-11-08
type: sessionprotokoll
source: opencode
model: opencode-go/glm-5.3-flash
tags:
  - sessionprotokoll
  - rollen
  - dokumentation
  - pilotvorbereitung
status: active
---

# Sessionprotokoll – 2026-11-08 Rollen-Hinweis Klonen

## Ausgangslage

- **Datum:** 2026-11-08 (Fortsetzung nach [[90-Index/Sitzungen/2026-10-29 vault-update Integration]])
- **Aktives OpenCode-Modell:** `opencode-go/glm-5.3-flash`
- **Letzter Commit (Sitzungsbeginn):** `f209170` (Teilnehmer-Git-Modell integriert)
- **Ziel der Sitzung:** Nutzeranforderung – Einsteiger müssen **gleich beim Klonen** auf den Unterschied Kursleiter/Teilnehmer gestoßen werden; der Unterschied war nur in [[10-Wissensbasis/GitHub-Repository]] beschrieben, ohne Verweis aus der README

## Analyse

Sitzungsvorbereitende Inventur: das Rollenmodell (Kursleiter = Lesen + Schreiben auf `origin/main`; Teilnehmer = nur-lesender Klon, Arbeit auf `mein-vault`, kein push, Kursneuerungen via `/vault-update`) war am 2026-10-29 vollständig in Command, Agenten-Regel und Kursdokumentation integriert. Die Lücke war **reine Sichtbarkeit**: README und Einstieg-Schritt 1 nannten „Repository holen" ohne jede Rollen-Erwähnung – ein Einsteiger liest erst in Schritt 7 vom nur-lesenden Klon.

## Was getan wurde

- **README.md:** neuer Abschnitt „🧑‍🏫 Rollen beim Klonen" (direkt nach der Einrichtung, vor dem Ziel) – Weichenstellungs-Formulierung („die wichtigste Weichenstellung für Einsteiger"), kompakte Rollentabelle (Kursleiter: Lesen+Schreiben, `main`, push; Teilnehmer: nur lesen, `mein-vault`, nie puschen, Kursneuerungen via `/vault-update`), Verweise auf [[10-Wissensbasis/GitHub-Repository]] und [[Einstieg]]
- **Einstieg.md** (Schritt-1-Zeile): „Rolle beachten: der Kursleiter pusht ins GitHub-Repo, Teilnehmer haben einen nur-lesenden Klon und arbeiten auf `mein-vault`" – direkter Link auf den Abschnitt „Rollenperspektiven" in GitHub-Repository.md; Verweis-Ziil von „README – Einrichtung" auf „README – Einrichtung & Rollen"
- **Einstieg.md (Landkarte):** README-Zeile um „Rollen beim Klonen" ergänzt
- Commit `57cf864` (Protokoll-Commit folgt)

### Nachtrag (Kurs-Tags, gleiche Sitzung)

- Inventur: `kurs-start` existierte bereits lokal **und** auf `origin`, zeigte aber auf `f209170` – also auf den Stand **ohne** den heutigen Rollen-Hinweis in README/Einstieg. Der Tag wurde auf HEAD verschoben: `git tag -f kurs-start HEAD` + `git push -f origin kurs-start` (sicher: der Pilot läuft noch nicht, niemand nutzt den Tag)
- Verifikation: `git ls-remote --tags origin` zeigt `refs/tags/kurs-start` auf `ce358be` ✓ – Teilnehmer klonen jetzt den Stand, der `/vault-update`, `/vault-reset`, die Rollen-Hinweise und die Archiv-Konvention vollständig enthält
- `kurs-update` wurde **bewusst nicht gesetzt**: der Tag-Name ist in keinem Material referenziert (genutzt wird nur `kurs-start`, z. B. `git diff kurs-start mein-vault` und `git switch -c versuch-2 kurs-start`). Falls künftige Kursiterationen einen „zuletzt ausgelieferten Stand" markieren wollen, wird der Tag zusammen mit der dokumentierten Konvention bei Bedarf in [[10-Wissensbasis/Git-Grundlagen]] ergänzt

### Nachtrag 2 (live-Test `/vault-update`, Evaluation, Pilot-Status – gleiche Sitzung)

- **Nutzerbestätigung:** `/vault-update` ist in einem **echten Teilnehmer-Zugang korrekt durchgelaufen** (Inventur, Merge, Konfliktentscheidungen) – der offene Punkt „in echten OpenCode-Sessions verifizieren" gilt damit als erfüllt
- **Evaluation „Checklisten als Vorlagen nach `90-Index/Templates/` auslagern" → Ergebnis: Nein, Status quo bleibt.** Begründung: Der reale Konfliktfall ist selten (der Kurs ändert Checkbox-Zeilen kaum; andereÄnderungshunks außerhalb der Checkbox-Zeilen mergen automatisch) und bereits elegant behandelt – pro-Datei-Empfehlungen inkl. `--theirs` + `/vault-reset`-Folgeschritt, live bestätigt (Nutzerdurchlauf). Die Auslagerung hätte den Merge-**Nutzen** zerstört (automatische Weiterreichung von Kurs-Iterationen in ausgefüllte Checklisten), erzeugt aber manuelle Synchronisationslast, Doppel-Verwaltung Vorlage/Kopie, neue Einstiegs-Friction und einen Umbau der `/vault-reset`-Startzustandsdefinition. Dazu läuft der Pilot bereits – keine Mid-Pilot-Umstrukturierung ohne gemessenen Bedarf. **Re-Evaluations-Kriterium:** nur bei Konflikt-Schwierigkeiten im Pilot-Feedback
- **Pilot läuft** (Nutzerangabe)

### Nachtrag 3 (Feedback-Flow, gleiche Sitzung)

**Nutzeridee:** Pilot-Feedback soll sich im **Eingang** (`00-Inbox/`) sammeln und es soll eine **Vorlage** geben, mit der Teilnehmer Änderungsvorschläge strukturiert einreichen können. Umgesetzt:

- **Neue Vorlage `90-Index/Templates/Feedback.md`:** Frontmatter-Felder `typ` (Verständnisfrage / Fehler / Verbesserung / neue Idee), `betreff` (Datei/Abschnitt), `status: offen`; Abschnitte Betreff / Ist / Vorschlag / Kontext; feste Fußzeilen-Regel: Notiz bleibt in `00-Inbox/`, bis der Kursleiter sie übernommen hat
- **Teilnehmer-Ablauf in [[Einstieg]]** (Abschnitt „Pilot-Feedback einreichen"): Anlegen via Quick Switcher → `Feedback`-Template einfügen → füllen → in `00-Inbox/` liegen lassen → Übergabe an den Kursleiter per Sitzung/Datei (kein push, im Modell ausgeschlossen)
- **Kursleiter-Ablauf:** Datei in die kursseitige `00-Inbox/` importieren → in neuem Sammel-MOC **`90-Index/Pilot-Feedback.md`** registrieren (Abschnitte Eingegangen/Verarbeitet) → verarbeitet: `status: verarbeitet`, Migration nach `20-Archiv/`, Erkenntnisse in die Leitfäden (Kurs-Iteration)
- **`/vault-reset` erweitert:** Phase 2 kennt Feedback-Notizen (tags `feedback`) und schlägt standardmäßig **Behalten** vor – Feedback wird vom Reset niemals weggeschlagen

**Verifikation:** Difference-Check der Struktur gegen das bestehende `Wissensnotiz`-Template (gleiche Platzhalter-Mechanik); Verweis-Kette geprüft: Einstieg → Templates/Feedback → Pilot-Feedback; `/vault-reset`-Regel deckt die Fußzeilen-Regel der Vorlage

### Nachtrag 4 (GitHub-Issue-Kanal als primärer Feedback-Weg, gleiche Sitzung)

**Nutzerentscheidung:** Für Teilnehmer-Feedback soll der **GitHub-Issue-Mechanismus** genutzt werden (Issues für Vorschläge ohne Code; Discussions für offene Fragen/Ideen) – statt nur Dateiübertragung per Sitzung.

**Infrastruktur (via `gh`-CLI, authentifiziert als Repobesitzer):**
- Repo-Prüfung: **public** → jeder Einsteiger kann Issues eröffnen/kommentieren (kein Zugangsproblem); Issues enabled; Discussions **aktiviert** (`gh repo edit --enable-discussions`)
- Label `feedback` erstellt („Rückmeldung zur Pilotphase")
- **`.github/ISSUE_TEMPLATE/feedback-vorschlag.md`** angelegt – gleiche Felder wie die lokale Vorlage (Betreff / Ist / Vorschlag / Kontext), Label-Assign `feedback`
- **`CONTRIBUTING.md`** im Repo-Root: Kanaltabelle (Issues für konkretes Feedback, Discussions für offene Fragen), Rollen-Zuordnung, Issue-Regeln, Kursleiter-Hinweise

**Modellabgrenzung (bewusst dokumentiert im CONTRIBUTING):** Der aus dem Nutzerzitat übernommene Fork/PR-Teil („Allow edits by maintainers", Zweig pro Änderung) trifft auf unser nur-lesendes Klon-Modell **nicht zu** – es gibt keine Teilnehmer-PRs; ein `PULL_REQUEST_TEMPLATE.md` wurde daher bewusst **nicht** angelegt. Re-Evaluation nur, falls das Modell später auf Fork+PR erweitert wird.

**Doku-Integration:** [[Einstieg]] (Abschnitt „Pilot-Feedback einreichen" umgebaut: Weg 1 Browser-Formular, Weg 2 `gh issue create --web`/`--title/--body`, Weg 3 lokale Vorlage als Entwurf/Fallback; Landkarte um `.github/` erweitert), [[10-Wissensbasis/GitHub-Repository]] (Teilnehmer-Beitragen-Absatz), [[90-Index/Pilot-Feedback]] (primär Issues, Fallback-Import), [[90-Index/Wissensindex]]. Der `/vault-reset`-Schutz für lokale Feedback-Notizen bleibt unverändert (Fallback-Kanal).

### Nachtrag 5 (Leitfaden „Feedback & Contributions beitragen", gleiche Sitzung)

**Nutzerwunsch:** Ein Leitfaden für **alle**, in der Wissensbasis hinterlegt und an allen passenden Stellen verlinkt (bisher verteilt auf Einstieg + CONTRIBUTING + Templates, ohne Sammel-Dokument).

- **Neu: `10-Wissensbasis/Feedback-Beitragen.md`** – drei Wege (Browser-Issue [empfohlen], `gh`-CLI, lokale Entwurfs-Vorlage als offline/Fallback), feste Kanalzuordnung (Issue / Discussions / entfallendes Material-Editing), Regeln für gute Meldungen, Kursleiter-Sicht (Label `feedback`, Sammel-MOC, Verarbeiten → schließen), Links
- **Verlinkt an allen Stationen:** [[90-Index/Wissensindex]] (Pilot-Feedback-Sektion, an erster Stelle), [[Einstieg]] (Feedback-Abschnitt), [[10-Wissensbasis/GitHub-Repository]] (Beitragen-Absatz), CONTRIBUTING (Tabellen-Fußzeile mit Pfad), `90-Index/Templates/Feedback.md` (Fußnote)
- **Eigenkontrolle:** Fremdschrift-Scan (CJK/Kyrillisch) über alle geänderten Dateien → 0 Treffer (nach mehreren Korrekturen in der Sitzung)
- Einstufung: **Hilfsnotiz**, keine Kernnotiz (der K2-Kanon von M1 bleibt unverändert auf den 5 Kernnotizen)

### Nachtrag 7 (Ordner-Link entfernt, gleiche Sitzung)

**Nutzerfund:** In der Einstieg-Landkarte linkte „[Sessionprotokollen](90-Index/Sitzungen/)" auf einen **Ordner** – Markdown-Links müssen aber auf Dateien zeigen (Obsidian kann Ordner nicht öffnen; Konvention: Links → Notizen/Dateien, Ordneransichten gibt es nur direkt in GitHub). Ersetzt durch die Formulierung „dort sind alle Sessionprotokolle verlinkt", da das Entwicklungsprotokoll bereits die Sitzungstabelle mit allen Links enthält. Volltext-Scan bestätigt: dieses Muster existierte nur an dieser einen Stelle.

### Nachtrag 8 (Kreuzverweise der Feedback-Vorlagen, gleiche Sitzung)

**Nutzeranforderung:** der fehlende Verweis auf die GitHub-„Änderungsvorschlag"-Vorlage gehört neben das Obsidian-Template. Umgesetzt:

- **`90-Index/`-Zeile:** die zwei Vorlagen-Varianten stehen jetzt mit Rollen-Label nebeneinander – „[Feedback-Vorlage (Obsidian)](90-Index/Templates/Feedback.md) & [Änderungsvorschlag (GitHub-Issue-Vorlage)](.github/ISSUE_TEMPLATE/feedback-vorschlag.md)"
- **`.github/`-Zeile:** umgekehrter Querverweis – „Entwurfs-Variante im Vault: [Feedback-Vorlage (Obsidian)](90-Index/Templates/Feedback.md)"
- **Begründung:** die zwei Templates sind zwei Varianten desselben Feedback-Zwecks (Betreff/Ist/Vorschlag): Obsidian-Vorlage = lokaler Entwurf + offline-Fallback (bleibt in `00-Inbox/`, `/vault-reset`-Schutz), GitHub-Issue-Vorlage = gerendertes Web-Formular (primärer Kanal). Beide immer zusammen sichtbar verhindert, dass ein Einsteiger nur eine von zwei gültigen Einreichungsvarianten entdeckt.

### Nachtrag 6 (Kanal-Anleitungen + Landkarten-Korrekturen, gleiche Sitzung)

**Nutzerhinweis:** In der Einstieg-Landkarte fehlten die Endverweise für die zwei Kanäle (Issues/Discussions) (Issues/Discussions) – und der Fehlhinweis lenkte auf zwei reale Mängel:
1. **Kaputter relativer Link** in der `.github/`-Zeile: `../.github/...` stieg aus dem Repo-Root aus (Einstieg.md liegt im Root!) – korrigiert zu `.github/ISSUE_TEMPLATE/feedback-vorschlag.md` (in Obsidian und GitHub-Render korrekt gültigen Pfaden)
2. **Feedback-Vorlage wurde in der `90-Index/`-Zeile textlich erwähnt, aber nicht verlinkt** – jetzt als eigener Link (`90-Index/Templates/Feedback.md`) alongside der Notiz-Vorlage

**Umsetzung (Nutzerentscheidung „Kanal-Doks je Kanal“):**
- **Neu: `10-Wissensbasis/GitHub-Issues-nutzen.md`** – Wofür/Wofür-nicht, die drei Wege (Browser / gh CLI / lokale Entwurfsnotiz), Issue-Regeln, Kursleiter-Sicht
- **Neu: `10-Wissensbasis/Discussions-nutzen.md`** – Abgrenzung zu Issues (Issue=konkret/handelbar vs. Discussion=explorativ), Ankündigung als Reife-Ze, public-Repo-Bewusstsein, Übergang Discussion→Issue
- **Landkarten-Verlinkung:** `.github/`-Zeile um die zwei Anleitungen erweitert; [[90-Index/Wissensindex]] listet beide im Pilot-Feedback-Abschnitt
- **Lebenszyklus-Regel konsistent:** eine Discussion läuft unbegrenzt weiter; reift sie zu einem konkreten Vorschlag, wird sie über einen verlinkten Issue materialisiert

## Probleme & Lösungen

### Rollenbinfo war tief im Material versteckt

**Symptom:** Einsteiger, die das Repo klonen, erfahren erst spät (Einstieg Schritt 7 / `/vault-update`-Abschnitt), dass sie nach Teilnehmer-Regeln arbeiten

**Ursache:** Die Rollenperspektiven standen in [[10-Wissensbasis/GitHub-Repository]], aber weder README noch der Klonschritt des Einstiegs verwiesen darauf

**Lösung:** Verweis-Kette geschlossen: README-Abschnitt (weichste Stufe für GitHub-Besucher) → Einstieg Schritt 1 → GitHub-Repository (Detail). Keinerlei Änderung am Modell selbst

**Verwerfte Ansätze:** Rolleninfo direkt in alle Leitfäden duplizieren – Redundanz; stattdessen das etablierte Muster „eine Quelle, viele Zielverweise"

**Verifikation:** Klick-Pfad geprüft: GitHub → README → Einstieg → GitHub-Repository; jeder Schritt erklärt die Rolle, bevor `git clone` fällt

## Artefakte (neu / geändert)

- `README.md` – Abschnitt „🧑‍🏫 Rollen beim Klonen"
- `Einstieg.md` – Schritt-1-Hinweis, Landkarten-Zeile
- Commit `57cf864`

## Entscheidungen

- **Modell unverändert** (gültig: 2026-10-29-Sitzung): nur Sichtbarkeit erhöht
- Platzierung im README **direkt nach der Einrichtung** (bevor der Nutzer `git clone` tippt), nicht versteckt in Fußnoten

## Nächste Schritte (Pickup für nächste Sitzung)

- [x] Tags `kurs-start`/`kurs-update` im Kurs-Repo setzen und pushen (offen seit 2026-10-29) – erledigt: `kurs-start` auf HEAD verschoben und gepusht; `kurs-update` bewusst nicht gesetzt (unreferenziert, siehe Nachtrag oben)
- [x] `/vault-update` in echten OpenCode-Sessions verifizieren – erledigt durch Nutzer (echter Teilnehmer-Zugang, Nachtrag 2)
- [x] Checklisten als Vorlagen nach `90-Index/Templates/` auslagern? – **Nein** (Evaluation → Nachtrag 2; Re-Evaluation nur bei Pilot-Feedback)
- [ ] Pilotdurchlauf: laufend Feedback sammeln (Pilot läuft bereits)
- [ ] Feedback-Flow live nutzen: erstes echtes Teilnehmer-Feedback über die neue Vorlage durchlaufen lassen (Einreichen → Import → Wissensindex/Sammlung → Verarbeiten)
- [ ] Ausgewähltes Pilot-Feedback zurück in die Materialien (Kurs-Iteration)

---

## Handoff (für Übergabe an nächste Sitzung)

**Zusammenfassung in 1–2 Sätzen:**

Der Rollen-Unterschied (Kursleiter pusht, Teilnehmer klonen nur-lesend) ist jetzt schon beim Klonen sichtbar: neuer README-Abschnitt „🧑‍🏫 Rollen beim Klonen" plus Verweis in Einstieg-Schritt 1 auf [[10-Wissensbasis/GitHub-Repository]]. Das Modell selbst blieb unverändert. Nachtrag 2: `/vault-update` live im Teilnehmer-Zugang bestätigt; Vorlagen-Auslagerung evaluiert → **Nein** (Status quo); **Pilot läuft**.

**Wichtigste Dateien/Commits:**

- Commit `57cf864` – README + Einstieg

**Modell:** `opencode-go/glm-5.3-flash`

**Offen für nächste Sitzung:**

- [ ] Pilotbegleitung: Feedback sammeln und Kuratieren
- [ ] Kurs-Iteration mit ausgewähltem Pilot-Feedback
