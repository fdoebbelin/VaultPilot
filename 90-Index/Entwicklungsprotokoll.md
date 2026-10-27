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

---

## Aktueller Handoff (Ende der letzten Sitzung)

- **Letzter Stand:** Commit `e4a2304` + Abschluss-Commit auf `origin/main` (`https://github.com/fdoebbelin/VaultPilot.git`) – **Projekt abgeschlossen:** alle Erfolgskriterien K1–K6 erfüllt, alle Meilensteine M1–M4 erreicht
- **Aktives OpenCode-Modell:** `opencode-go/glm-5.3-flash` (Wechsel von `opencode/nemotron-3.5-super-vl-free`)
- **Phase:** ✅ Umsetzung abgeschlossen (Phase A–D); Detaildokumentation: [[90-Index/Sitzungen/2026-10-27 Umsetzungsabschluss]], Statusübersicht: [[Abschlussbericht]]
- **Hinweis:** Kein CLI-Befehl `opencode model` vorhanden; Modell-Wechsel nur über OpenCode TUI (`Ctrl+X` → `m`) oder Config-Datei
- **Hinweis:** Repository-Pfad immer über `$env:VAULTPILOT` adressieren (Einrichtung siehe README, Abschnitt „Einrichtung"); hartcodierte Benutzerpfade sind verboten
- **Hinweis:** `$env:VAULTPILOT` ist dauerhaft im User-Scope gesetzt; die Variable steht erst in Prozessen zur Verfügung, die **nach** dem Setzen gestartet wurden – notfalls Terminal komplett neu starten
- **Hinweis:** Auf anderen Geräten wird `workspace.json` beim nächsten `git pull` aus dem Repo gelöscht – Obsidian legt sie beim ersten Start automatisch neu an (harmlos)
- **Offene Punkte (nächste Projektphase):**
  - [ ] Pilotdurchlauf des Kurses mit echten Teilnehmern
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
- [[90-Index/Wissensindex]] – MOC über die Wissensbasis
