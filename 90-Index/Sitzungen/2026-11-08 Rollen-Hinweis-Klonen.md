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
