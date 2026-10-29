---
title: GitHub-Repository – Einrichtung & Workflow
tags: [github, git, repository, devops, dokumentation]
created: 2026-10-26
updated: 2026-10-29
---

# GitHub-Repository – Einrichtung & Workflow

## Ziel

VaultPilot als GitHub-Projekt versionieren und bereitstellen – und die **Teilnehmer-Seite**: Abrufen des Kurs-Repos als Klon.

## Rollenperspektiven

### Kursleiter (Repobesitzer)

1. **GitHub-Repository erstellen**
   - Auf github.com → *New repository*
   - Name: z. B. `VaultPilot`
   - Public oder Private

2. **Remote lokal einrichten**
   ```bash
   git remote add origin https://github.com/<USER>/VaultPilot.git
   git branch -M main
   git push -u origin main
   ```

3. **Änderungen verwalten**
   - Commits lokal: `git add -A` + `git commit -m "..."`
   - Pushen: `git push`
   - Kurs-Tags (Referenzpunkte für Teilnehmer) setzen und veröffentlichen: `git tag kurs-start` + `git push --tags`

### Teilnehmer (nur lesender Klon)

Teilnehmer haben **keine Schreibrechte** auf das Kurs-Repo – `origin` dient rein zum Lesen:

```bash
git clone https://github.com/fdoebbelin/VaultPilot.git $env:VAULTPILOT
cd $env:VAULTPILOT
git config user.name  "Vorname Nachname"
git config user.email "name@example.org"
git switch -c mein-vault
```

| Branch | Inhalt | Regel |
|---|---|---|
| `main` | Kursstand | Spiegel von `origin/main` – nie committen |
| `mein-vault` | eigene Notizen, Daily Notes, Häkchen | hier arbeiten und committen – nie pushen |

Kursneuerungen kommen nicht per `pull`, sondern über den Command `/vault-update` (fetch + merge mit Inventur, Konflikt-Vorschau und Bestätigung). Details: [[10-Wissensbasis/Git-Grundlagen]] und [[Einstieg]].

## Projektbezogene Einordnung

- Repo enthält: Konzept, Agenda, Wissensnotizen, Agent-Konfiguration, Vault-Struktur
- Versionierung begleitet Implementierung & Tests
- GitHub als Ort der **Verteilung der Wissensbasis** (Teilziel 5)

## Status

✅ Erledigt: Remote `https://github.com/fdoebbelin/VaultPilot.git` eingerichtet, erste Veröffentlichung gepusht. Der Workflow der **Teilnehmer** (Klon, `mein-vault`, `/vault-update` statt pull/push) ist in [[10-Wissensbasis/Git-Grundlagen]] und [[Einstieg]] beschrieben.

## Links

- [[10-Wissensbasis/Git-Grundlagen]]
- [[Einstieg]]
- [[VaultPilot – Konzept]]
- [[90-Index/Wissensindex]]
