---
title: Entwicklungsprotokoll VaultPilot
created: 2026-10-26
updated: 2026-10-27
type: entwicklungsprotokoll
tags:
  - entwicklungsprotokoll
  - vaultpilot
status: active
---

# Entwicklungsprotokoll VaultPilot

## Zweck

Zentrale Übersicht aller Entwicklungssitzungen. Jede Sitzung wird hier **kurz zusammengefasst** und auf das detaillierte **Sessionprotokoll** im Unterverzeichnis `90-Index/Sitzungen/` verlinkt.

Das detaillierte Sessionprotokoll wird bei Bedarf erzeugt (z. B. bei einem **Handoff**), damit das Kontextfenster klein bleibt und eine neue Session – auch auf einem anderen Rechner – nahtlos anknüpfen kann.

## Sitzungen (chronologisch)

| Datum | Thema | Sessionprotokoll | Status |
|-------|-------|------------------|--------|
| 2026-10-26 | Projekt-Vorbereitung, Vault-Aufbau, Agenten-Workflow, GitHub-Publish, Sitzungsprotokoll | [[90-Index/Sitzungen/2026-10-26 VaultPilot-Protokoll]] | abgeschlossen |
| 2026-10-26 | Umsetzung: Obsidian-Auswertung, erste Daily Note | [[90-Index/Sitzungen/2026-10-26 Umsetzung Obsidian-Auswertung]] | abgeschlossen |
| 2026-10-27 | Git-Hygiene: arbeitsplatzbezogene Obsidian-Konfiguration ausgeschlossen | [[90-Index/Sitzungen/2026-10-27 Git-Ignore-Arbeitsplatzkonfiguration]] | abgeschlossen |
| 2026-10-27 | Leitfäden: Obsidian-Installation & Obsidian-Grundlagen (Checkliste A.3/C.0) | [[90-Index/Sitzungen/2026-10-27 Obsidian-Leitfäden]] | abgeschlossen |
| 2026-10-27 | Pfadneutralisierung: `$env:VAULTPILOT` in Richtlinien & Leitfäden | [[90-Index/Sitzungen/2026-10-27 Pfadneutralisierung]] | abgeschlossen |
| 2026-10-27 | Konzept finalisiert (CONCEPT.md v2, M1 erfüllt) | [[90-Index/Sitzungen/2026-10-27 Konzeptfinalisierung]] | abgeschlossen |
| 2026-10-27 | Umsetzungsabschluss: Kernnotizen (K2), MOC (K3), Abschlussbericht | [[90-Index/Sitzungen/2026-10-27 Umsetzungsabschluss]] | abgeschlossen |
| 2026-10-29 | Einstiegsdokument + Command `/vault-reset` (definierter Startpunkt) | [[90-Index/Sitzungen/2026-10-29 Einstieg-und-vault-reset]] | abgeschlossen |
| 2026-10-29 | Command `/vault-update` integriert (Teilnehmer-Git-Modell) | [[90-Index/Sitzungen/2026-10-29 vault-update Integration]] | abgeschlossen |
| 2026-11-08 | Rollen-Hinweis beim Klonen (README + Einstieg) | [[90-Index/Sitzungen/2026-11-08 Rollen-Hinweis-Klonen]] | abgeschlossen |
| 2026-10-29 | Teilnehmer-Git-Modell: Command `/vault-update` integriert, Kursdokumentation umgestellt, Testszenarien (Konflikt + Rettung) | [[90-Index/Sitzungen/2026-10-29 vault-update Integration]] | abgeschlossen |

---

## Aktueller Handoff (Ende der letzten Sitzung)

- **Letzter Stand:** Commit `57cf864` (+ Protokoll-Commit) auf `main` (`https://github.com/fdoebbelin/VaultPilot.git`) – Rollen-Hinweis beim Klonen: README-Abschnitt „🧑‍🏫 Rollen beim Klonen" + Verweis in Einstieg-Schritt 1; damit ist das Teilnehmer-Git-Modell (vom 2026-10-29) schon beim ersten Klonen sichtbar
- **Aktives OpenCode-Modell:** `opencode-go/glm-5.3-flash`
- **Phase:** Pilotvorbereitung – Umsetzung abgeschlossen; Teilnehmer-Workflow (kein push, kein pull, `mein-vault`) ist in den Materialien verankert. Detailprotokolle: [[90-Index/Sitzungen/2026-10-29 vault-update Integration]] (Modell), [[90-Index/Sitzungen/2026-11-08 Rollen-Hinweis-Klonen]] (Sichtbarkeit)
- **Hinweis:** `/vault-update check|apply` ist erfolgreich getestet in einem simulierten Teilnehmer-Repo (Inventur, Konflikt-Vorschau, Merge mit Konfliktentscheidung `--theirs`, Rettung versehentlicher main-Commits). Noch nicht in einer echten OpenCode-Session mit Agenten-Ausführung getestet.
- **Hinweis:** Reihenfolge für Teilnehmer: erst `/vault-update` (Kursstand holen), dann `/vault-reset` (Startpunkt herstellen) – beide Commands arbeiten an denselben Übungsdateien.
- **Hinweis:** Kein CLI-Befehl `opencode model` vorhanden; Modell-Wechsel nur über OpenCode TUI (`Ctrl+X` → `m`) oder Config-Datei
- **Hinweis:** Repository-Pfad immer über `$env:VAULTPILOT` adressieren (Einrichtung siehe README, Abschnitt „Einrichtung"); hartcodierte Benutzerpfade sind verboten
- **Hinweis:** `$env:VAULTPILOT` ist dauerhaft im User-Scope gesetzt; die Variable steht erst in Prozessen zur Verfügung, die **nach** dem Setzen gestartet wurden – notfalls Terminal komplett neu starten
- **Offene Punkte (nächste Projektphase):**
  - [x] ~~Tags `kurs-start`/`kurs-update`~~ erledigt 2026-11-08: `kurs-start` auf HEAD verschoben (`ce358be`) und gepusht; `kurs-update` bewusst nicht gesetzt (in Materialien unreferenziert)
  - [ ] `/vault-update` in echten OpenCode-Sessions verifizieren (Agent befolgt den Markdown-Command)
  - [ ] Pilotdurchlauf des Kurses mit echten Teilnehmern
  - [ ] Checklisten als Vorlagen nach `90-Index/Templates/` auslagern? (strukturelle Konfliktvermeidung, separat entscheiden)
  - [ ] Erfahrungswerte aus dem Piloten zurück in die Materialien (Kurs-Iteration)

---

## Handoff / Pickup – Workflow

### Handoff (Ende einer Sitzung)

1. Erstelle ein detailliertes Sessionprotokoll im Unterverzeichnis `90-Index/Sitzungen/`:
   - Dateiname: `JJJJ-MM-TT <Thema>.md` (z. B. `2026-10-27 Umsetzung OpenCode-Setup.md`)
   - Vorlage: `[[90-Index/Handoff-Pickup-Vorlage]]`
2. Trage oben in dieser Tabelle eine neue Zeile ein (Datum, kurzes Thema, Verlinkung, Status).
3. Aktualisiere den **Aktuellen Handoff**-Block oben mit dem neuesten Stand.
4. Committe und pushe alles auf `origin/main`.

### Pickup (Beginn einer neuen Sitzung)

1. Lies den **Aktuellen Handoff** oben.
2. Öffne das verlinkte Sessionprotokoll für Details.
3. Setze bei den **Offenen Punkten** fort.
4. Arbeite im Projekt und beende mit einem neuen Handoff.

---

## Links

- [[90-Index/Handoff-Pickup-Vorlage]] – Vorlage für Sessionprotokolle und Übergaben
- [[90-Index/Sitzungen/2026-10-26 VaultPilot-Protokoll]] – detailliertes Protokoll der ersten Sitzung
- [[90-Index/Sitzungen/2026-10-26 Umsetzung Obsidian-Auswertung]] – Protokoll der Umsetzungssitzung
- [[90-Index/Sitzungen/2026-10-27 Git-Ignore-Arbeitsplatzkonfiguration]] – Protokoll der Git-Hygiene-Sitzung
- [[90-Index/Sitzungen/2026-10-27 Obsidian-Leitfäden]] – Protokoll der Obsidian-Leitfäden-Sitzung
- [[90-Index/Sitzungen/2026-10-27 Pfadneutralisierung]] – Protokoll der Pfadneutralisierung
- [[90-Index/Sitzungen/2026-10-27 Konzeptfinalisierung]] – Protokoll der Konzeptfinalisierung
- [[90-Index/Sitzungen/2026-10-27 Umsetzungsabschluss]] – Protokoll des Umsetzungsabschlusses
- [[90-Index/Sitzungen/2026-10-29 Einstieg-und-vault-reset]] – Protokoll Einstieg & vault-reset
- [[90-Index/Wissensindex]] – MOC über die Wissensbasis
