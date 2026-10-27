---
title: GitHub-Repository – Einrichtung & Workflow
tags: [github, git, repository, devops, dokumentation]
created: 2026-10-26
updated: 2026-10-27
---

# GitHub-Repository – Einrichtung & Workflow

## Ziel

VaultPilot als GitHub-Projekt versionieren und bereitstellen.

## Schritte

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

## Projektbezogene Einordnung

- Repo enthält: Konzept, Agenda, Wissensnotizen, Agent-Konfiguration, Vault-Struktur
- Versionierung begleitet Implementierung & Tests
- GitHub als Ort der **Verteilung der Wissensbasis** (Teilziel 5)

## Status

✅ Erledigt: Remote `https://github.com/fdoebbelin/VaultPilot.git` eingerichtet, erste Veröffentlichung gepusht. Der tägliche Workflow (pull/commit/push) ist in [[10-Wissensbasis/Git-Grundlagen]] beschrieben.

## Links

- [[10-Wissensbasis/Git-Grundlagen]]
- [[VaultPilot – Konzept]]
- [[90-Index/Wissensindex]]
