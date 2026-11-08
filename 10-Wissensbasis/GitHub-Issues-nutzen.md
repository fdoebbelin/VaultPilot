---
title: GitHub-Issues nutzen (Kanal-Anleitung)
created: 2026-11-08
updated: 2026-11-08
tags:
  - github
  - issues
  - feedback
  - pilot
status: active
---

# GitHub-Issues nutzen (Kanal-Anleitung)

## Zweck

Der Kanal für **Vorschläge ohne Code**: Fehlermeldungen, Fragen-Feedback und Verbesserungsideen zu den Kursmaterialien. Die Rolle „Read“/public-Zugriff reicht – Issues eröffnen und kommentieren kann jeder ohne Schreibrechte am Repo.

## Wofür (und wofür nicht)

| Passend | Nicht passend |
|---|---|
| „Beispiel X in Übung Y funktioniert so nicht" | Offene Frage ohne konkreten Vorschlag → [[10-Wissensbasis/Discussions-nutzen]] |
| „In Leitfaden Z wird Schritt 3 missverständlich" | Idee ohne Vorschlagskern → Discussions |
| „Regel A widerspricht Regel B" | Eigenes Umschreiben des Kursmaterials (Rollenrahmen – siehe [[CONTRIBUTING]]) |

## Drei Wege zum Issue

### 1. Browser (empfohlen)

Repository → Tab **Issues** → **New issue** → Template **„Feedback / Änderungsvorschlag"** wählen → Felder füllen → Submit. Das Label `feedback` setzt sich automatisch.

### 2. `gh`-CLI

```powershell
gh issue create --web --repo fdoebbelin/VaultPilot      # Formular im Browser öffnen
gh issue create --repo fdoebbelin/VaultPilot --title "Kurztitel" --body "Betreff: ...`nIst: ...`nVorschlag: ..."
gh issue list --repo fdoebbelin/VaultPilot               # offene Issues einsehen
```

### 3. Lokale Entwurfs-Notiz (offline/Fallback)

`90-Index/Templates/Feedback.md` einfügen, ausfüllen (Betreff / Ist / Vorschlag / Kontext), Notiz bleibt in `00-Inbox/` – danach Inhalt per Copy-Paste ins Issue heben oder die Datei dem Kursleiter geben (er importiert sie in seine Inbox, siehe [[90-Index/Pilot-Feedback]]). `/vault-reset` schlägt für diese Notizen „behalten" vor.

## Regeln für gute Issues

- **Ein Thema pro Issue**
- Felder ausfüllen: **Betreff** (Datei/Abschnitt) · **Ist** (was erlebst du?) · **Vorschlag** (wie sollte es sein?)
- **Wortlaut belegen** statt paraphrasieren – „Vertrauen durch Verifikation" gilt auch für Meldungen
- Konstruktiv: Ist-Zustand vor dem Vorschlag nennen

## Kursleiter-Sicht

- Inventur: `gh issue list --repo fdoebbelin/VaultPilot --label feedback`
- Bearbeitungsstand im Vault: [[90-Index/Pilot-Feedback]] (Sammel-MOC)
- Verarbeiten: Issue kommentieren → schließen → Erkenntnis in die betroffene Leitfadenstelle ([[10-Wissensbasis/Feedback-Beitragen]] fasst den Ablauf zusammen)

## Links

- [[10-Wissensbasis/Feedback-Beitragen]] – Gesamt-Leitfaden aller Rollen und Wege
- [[CONTRIBUTING]] – Routing-Tabelle und Regeln
- [[90-Index/Templates/Feedback]] – lokale Entwurfs-Vorlage
- [[90-Index/Pilot-Feedback]] – Bearbeitungsstand im Vault
- [[10-Wissensbasis/GitHub-Repository]] – Rollenperspektiven
