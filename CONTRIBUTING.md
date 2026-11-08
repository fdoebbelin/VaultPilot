# Beiträge zum VaultPilot-Kurs

Wie du zum Kursmaterial beitragen kannst – abgestimmt auf das Rollenmodell ([README – Rollen beim Klonen](README.md) bzw. `10-Wissensbasis/GitHub-Repository.md`):

## Rollen

| Rolle | Verhältnis zu `origin` | Beitragskanal |
|---|---|---|
| **Kursleiter** (Repobesitzer) | Lesen + Schreiben (`main`), pusht Material-Updates | Commits, Labels, Issues pflegen |
| **Teilnehmer** | **nur-lesender Klon** (`mein-vault`, kein push) | **Issues** und **Discussions** |

## Kanäle

| Anliegen | Kanal |
|---|---|
| Fehler melden, Verbesserungsvorschläge, konkrete Feedbacks | **Issue** mit Template „Feedback / Änderungsvorschlag" |
| Offene Fragen, Ideen **ohne** konkreten Vorschlag | **Discussions** |
| Kursteilnehmer-Code-Änderungen am Kursrepo | entfällt im Modell – der nur-lesende Klon schließt Fork-/PR-Verfahren aus; das Kursmaterial pflegt der Kursleiter |

Ausführlicher Leitfaden für alle Rollen (Wege 1–3 mit Befehlen, Regeln und Kursleiter-Sicht): `10-Wissensbasis/Feedback-Beitragen.md`

## Regeln für gute Issues

- Ein **Thema pro Issue** – nicht mehrere Anliegen mixen
- Die Felder füllen: **Betreff** (Datei/Abschnitt) · **Ist** (was erlebst du?) · **Vorschlag** (wie sollte es sein?)
- Wortlaut belegen statt paraphrasieren („Vertrauen durch Verifikation")
- Feedback über das eigene `mein-vault`-Notizelement möglich: Entwurf mit `90-Index/Templates/Feedback.md`, dann Inhalt ins Issue übertragen (die Notiz bleibt in `00-Inbox/` – `/vault-reset` schlägt dafür „behalten" vor)

## Für den Kursleiter

- Repo ist **public** → alle Kursteilnehmer (und Interessierte) können Issues eröffnen/kommentieren, ohne Schreibrechte
- Labels: `feedback` (Pilotphase), daneben Standard-Labels (`bug`, `documentation`, …)
- Bearbeitungsstand: `90-Index/Pilot-Feedback.md` (Sammel-MOC im Vault); verarbeitete Issues schließen mit Kommentar, Erkenntnisse fließen in die Leitfäden (Kurs-Iteration)
- Discussions im Repo aktiviert (2026-11-08)

## Workflow-Verweis

Ablauf für Einsteiger: `Einstieg.md` · Teilnehmer-Git-Modell und `/vault-update`: `10-Wissensbasis/GitHub-Repository.md`
