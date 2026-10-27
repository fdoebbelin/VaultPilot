---
title: VaultPilot – Konzept
created: 2026-10-26
updated: 2026-10-27
tags:
  - konzept
  - vaultpilot
  - wissensmanagement
status: final
---

# VaultPilot – Konzept

## Überblick

**VaultPilot** begleitet den Kurs zur Arbeit mit agentischer KI am Beispiel von OpenCode. Im Fokus steht der **Aufbau und die Verwaltung eines Obsidian Vaults** zum **Wissensmanagement**.

Die Wissensbasis des Kurses selbst wird als praktisches Lern- und Arbeitsprojekt genutzt.

## Projektziele

### Zentrales Projektziel

Wissen strukturiert ablegen, vernetzen und dauerhaft pflegen – unterstützt und automatisiert durch einen KI-Agenten.

### Teilziele

1. **Installation & Setup:** Funktionierende Windows-Umgebung (PowerShell + scoop), Installation der benötigten Tools (OpenCode, Obsidian, Git), Schritt-für-Schritt-Anleitung für Teilnehmer.
2. **Einführung KI-Agent:** Abgrenzung KI-Chat vs. KI-Agent, Funktionsweise (Ziel → Plan → Tool-Use → Iteration), Vergleich und kritische Würdigung.
3. **Aufbau Wissensbasis:** Der Agent erstellt, strukturiert und vernetzt Wissensbasis-Notizen im Obsidian Vault.
4. **Einsatz Obsidian als Auswertung:** Nutzung von Obsidian als zentrale Sicht auf die Wissensbasis (Durchsuchen, Verwalten, Auswerten).
5. **Verteilung & Versionierung:** Versionierung der Wissensbasis über ein GitHub-Repository (clone/pull/push-Workflow, arbeitsplatzneutrale Pfad-Konvention), Dokumentation und Zugänglichkeit der Wissensbasis.

### Didaktische Ziele

- Verständnis dafür, wie ein Agent plant und iteriert
- Fähigkeit, Agenten-Aussagen kritisch zu prüfen
- Sicherer Umgang mit KI-Agenten in eigenen Projekten
- Transfer auf reale Wissensmanagement-Szenarien

## Abgrenzungen – Was ist kein Projektziel?

| Abgrenzung | Begründung |
|---|---|
| **Keine Plugin-Entwicklung** (eigene Obsidian-/Community-Plugins) | Core-Plugins + Git decken den Kursbedarf ab; Plugin-Entwicklung würde den Fokus verwässern und den Wartungsaufwand erhöhen. Community-Plugins bleiben höchstens ein Ausblick. |
| **Kein Obsidian Sync** (kostenpflichtiges Abo) | Synchronisation läuft bewusst über Git/GitHub – das ist zugleich Lehrinhalt (Teilziel 5). |
| **Keine Mobile-Einrichtung** | Kurs konzentriert sich auf Desktop unter Windows. |
| **Kein macOS/Linux** | Der Kurs ist Windows-basiert (PowerShell + scoop); andere Plattformen werden nicht behandelt. |

## Outcome & Meilensteine

| Meilenstein | Beschreibung | Status |
|---|---|---|
| **M1** | Konzept finalisiert und an das Niveau der Zielgruppe angepasst (dieses Dokument) | ✅ |
| **M2** | Installation, Einführung und Wissensbasis-Aufbau umgesetzt (Checkliste Phase A + C.0) | ✅ (2026-10-27, Übungsnachweis) |
| **M3** | Agenten-Workflow mit OpenCode etabliert (`/vault-new`, `/vault-link`, `/vault-index`) | ✅ (Phase B) |
| **M4** | Obsidian als Auswertungsfläche genutzt (Checkliste Phase C) | ✅ (2026-10-27) |

## Erfolgskriterien & Messbarkeit

Die Messbarkeit ist **checklisten-basiert**: Maßgeblich ist die [[10-Wissensbasis/Umsetzung-Checkliste]]; alle Kriterien sind objektiv prüfbar (durch Teilnehmer oder Agent).

- **K1 – Checkliste vollständig:** Alle Punkte der Umsetzung-Checkliste (Phasen A–D) abgehakt, mit Verifikationsnachweisen (Befehlsausgaben, Dateiexistenz).
- **K2 – Wissensbasis-Umfang:** Mindestens **5–7 Kernnotizen** zu den Kursinhalten (KI-Agent vs. Chat, OpenCode-Setup, Git-Grundlagen, Obsidian-Grundlagen, Agenten-Workflow), jede mit Frontmatter und mindestens einem `[[Wikilink]]`.
- **K3 – Struktur konform:** Ordner `00-Inbox/`, `10-Wissensbasis/`, `90-Index/` genutzt; ein MOC in `90-Index/` verlinkt alle Kernnotizen.
- **K4 – Agenten-Workflow funktionsfähig:** Die drei Commands erstellen/vernetzen/indizieren Notizen korrekt (durch Phase B verifiziert).
- **K5 – Verteilung funktioniert:** Repository auf GitHub gepusht; arbeitsplatzbezogene Dateien über `.gitignore` ausgeschlossen; Pfad-Konvention `$env:VAULTPILOT` dokumentiert ([[90-Index/Sitzungen/2026-10-27 Pfadneutralisierung]]).
- **K6 – Auswertung verifiziert:** Vault in Obsidian geöffnet, Core-Plugins aktiv, Daily Note mit Wikilinks, Backlinks-Ansicht geprüft.

## Zielgruppenbezug

- **Zielgruppe:** Fachinformatiker aller Richtungen im 2. Ausbildungsjahr
- **Voraussetzungen (Annahmen):** Windows-Grundkenntnisse, elementare PowerShell-Befehle, Umgang mit Dateisystem und Editor; Git-Grundkenntnisse sind hilfreich, aber nicht erforderlich (clone/add/commit/push werden im Kurs vermittelt)
- **Lernziele für Teilnehmer:**
  1. Das Agenten-Prinzip (Ziel → Plan → Tool-Use → Iteration) verstehen und Ergebnisse kritisch prüfen
  2. Entwicklungswerkzeuge selbst installieren (scoop, OpenCode, Obsidian, Git)
  3. Wissensnotizen mit Struktur (Ordner, Frontmatter, Tags) anlegen und vernetzen
  4. Obsidian als Auswertungsfläche nutzen (Suche, Backlinks, Graph, MOCs)
  5. Einen Git-basierten Synchronisations-Workflow für Wissen anwenden
- **Didaktischer Ansatz:** Der Agent führt vor, die Teilnehmer verifizieren anhand Checklisten („Vertrauen durch Verifikation") – das trainiert zugleich die kritische Würdigung von Agenten-Ausgaben.

## Umsetzungsplan

Die Umsetzung erfolgt entlang der [[10-Wissensbasis/Umsetzung-Checkliste]]:

- **Phase A:** Installation & Setup (OpenCode, Repository, Obsidian)
- **Phase B:** Erster Agenten-Workflow-Test
- **Phase C:** Obsidian als Auswertungsfläche (inkl. C.0 Grundlagen)
- **Phase D:** Dokumentation & Commit (Sessionprotokolle, Entwicklungsprotokoll, Push)

Sitzungsdokumentation: [[90-Index/Entwicklungsprotokoll]] (Handoff/Pickup-Workflow).

## Nächste Schritte

- [x] ~~C.0-Übungen durchlaufen + Backlinks-Ansicht prüfen~~ (erledigt 2026-10-27)
- [x] Wissensbasis auf 5–7 Kernnotizen ausbauen (K2) – erledigt
- [x] Abschlussbericht finalisieren – erledigt
- [ ] Pilotdurchlauf des Kurses mit Teilnehmern

---

Status: ✅ Konzept finalisiert & Umsetzung abgeschlossen (2026-10-27)
