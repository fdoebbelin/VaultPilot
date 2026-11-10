---
title: Feedback & Contributions beitragen (Issues, Discussions, Vorlage)
created: 2026-11-08
updated: 2026-11-08
tags:
  - feedback
  - github
  - issues
  - pilot
  - mitwirkung
status: active
---

# Feedback & Contributions beitragen

## Zweck

Der regulierte Weg, wie **alle Rollen** (Kursleiter, Teilnehmer, Interessierte) Feedback und Beiträge zum Kursmaterial einreichen – Kernaussage: **Code-Rechte sind nicht nötig.** Routing aller Fälle kompakt: [CONTRIBUTING.md](../CONTRIBUTING.md).

## Rollen & Kanäle (Kurzfassung)

| Rolle | Verhältnis zu `origin` | Kanäle |
|---|---|---|
| **Kursleiter** (Repobesitzer) | Lesen + Schreiben (`main`, push) | Commits, Labels, Issues/Discussions pflegen |
| **Teilnehmer** | nur-lesender Klon (`mein-vault`, kein push) | **Issues**, **Discussions** |
| **Interessierte** (public Repo) | nur lesen | **Issues**, **Discussions** |

**Feste Zuordnung: welches Anliegen in welchen Kanal?**

| Anliegen | Kanal |
|---|---|
| Fehler melden, konkrete Verbesserungsvorschläge | **Issue** (Template „Feedback / Änderungsvorschlag") |
| Offene Fragen, Ideen **ohne** konkreten Vorschlag | **Discussions** |
| „Kann ich das Kursmaterial selbst ändern?" | entfällt – nur-lesende Rollen editieren das Kursrepo nicht; das Kursmaterial pflegt der Kursleiter |

## Weg 1 – Issue im Browser (empfohlen, kein Tool nötig)

1. Repository öffnen: github.com/fdoebbelin/VaultPilot → Tab **Issues** → **New issue**
2. Template **„Feedback / Änderungsvorschlag"** wählen (liegt in `.github/ISSUE_TEMPLATE/feedback-vorschlag.md`)
3. Felder füllen:
   - **Betreff** – Datei/Abschnitt, z. B. „Einstieg.md, Schritt 3"
   - **Ist** – was du erlebt/gelesen hast, konkret mit Wortlaut
   - **Vorschlag** – wie es sein sollte, in eigenen Worten
   - **Kontext** (optional) – Umgebung, Situation
4. Titel prägnant machen, Submit – das Label `feedback` wird automatisch gesetzt

## Weg 2 – `gh`-CLI (Terminal, für Fortgeschrittene)

```powershell
gh issue create --web --repo fdoebbelin/VaultPilot      # Formular im Browser öffnen
# oder komplett im Terminal:
gh issue create --repo fdoebbelin/VaultPilot --title "Kurztitel" --body "Betreff: ...`nIst: ...`nVorschlag: ..."

gh issue list --repo fdoebbelin/VaultPilot              # offene Issues sehen
gh issue view <nummer> --repo fdoebbelin/VaultPilot     # Details lesen
```

## Weg 3 – lokale Entwurfs-Notiz (offline/Fallback)

Ohne GitHub-Konto im Unterricht oder als Vorstufe:

1. Notiz anlegen: `Strg+O` → Namen vergeben (z. B. `Feedback Verstehen Übung 5`) → Template `Feedback` einfügen (liegt in `90-Index/Templates/Feedback.md`)
2. Ausfüllen wie oben (Betreff / Ist / Vorschlag)
3. **Zwei Wege zum Ziel:**
   - Inhalt per Copy-Paste in ein Issue heben (Weg 1/2) – bevorzugt
   - oder die Notiz dem Kursleiter direkt geben; er importiert sie in seine `00-Inbox/` (Fallback-Registrierung siehe [[90-Index/Pilot-Feedback]])

Die Notiz **bleibt in `00-Inbox/`** – `/vault-reset` schlägt für Feedback-Notizen „behalten" vor, niemals löschen/archivieren.

## Regeln (was eine gute Meldung ausmacht)

- **Ein Thema pro Issue** – keine Anliegen mixen
- **Wortlaut belegen** statt paraphrasieren: Datei, Abschnitt, was genau auffällt („Vertrauen durch Verifikation")
- **Konstruktiv formulieren:** Ist-Zustand zuerst, Vorschlag danach – nicht „das ist Murks", sondern „so wie es dasteht, verstehe ich X; verstanden wäre eher Y"
- **Rollenrahmen respektieren:** Das Kursmaterial setzt der Kursleiter um – dein Beitrag ist die Meldung, nicht der Patch

## Kursleiter-Sicht (Bearbeitungsstand)

- Neue Issues erkennbar am Label `feedback`: `gh issue list --repo fdoebbelin/VaultPilot --label feedback`
- Bearbeitungsstand im Vault: [[90-Index/Pilot-Feedback]] (Issue-Zustand + Fallback-Importe aus Weg 3)
- Verarbeiten: Issue kommentieren → **schließen** → Erkenntnis in die betroffene Leitfadenstelle einarbeiten (Kurs-Iteration); Git-spezifische Treffer zusätzlich in die Problemtabelle von [[10-Wissensbasis/Git-Grundlagen]]
- Vor jedem kurseigenen Material-Commit kurz offene Issues prüfen – ein Issue dokumentiert manchmal bereits die passende Lösung

## Wo läuft das im Vault zusammen?

- [[90-Index/Pilot-Feedback]] – Sammel-MOC (Issues + Fallback-Importe)
- [[90-Index/Templates/Feedback]] – die lokale Entwurfs-Vorlage
- [CONTRIBUTING.md](../CONTRIBUTING.md) – Routing-Tabelle und Regeln
- [[Einstieg]] – Abschnitt „Pilot-Feedback einreichen" (kompakte Teilnehmer-Sicht)
- [[10-Wissensbasis/GitHub-Repository]] – Rollenperspektiven und Feedback-Kanal

## Verwandt

- [[10-Wissensbasis/Git-Grundlagen]] – Teilnehmerteil des Git-Modells (kein push, `mein-vault`)
- [[KI-Agent-vs-Chat]] – Kurswissen, das über Feedback läuft
- [[90-Index/Wissensindex]] – MOC
