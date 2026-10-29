# VaultPilot

**VaultPilot** – Dein KI-Agent für dein zweites Gehirn.

## Überblick

Ein Kursprojekt zur Arbeit mit **agentischer KI** am Beispiel von **OpenCode**. Der Fokus liegt auf dem **Aufbau und der Verwaltung eines Obsidian Vaults** zum **Wissensmanagement**.

**Neu hier?** → [Einstieg für Außenstehende](Einstieg.md) – Einstiegspunkt, Schritt-für-Schritt-Weg und definierten Startpunkt (`/vault-reset`) erklärt.

## ⚙️ Einrichtung

Das Repository wird über eine PowerShell-Umgebungsvariable adressiert – so funktionieren alle Leitfäden unabhängig vom Benutzernamen:

```powershell
# Einmalig einrichten (dauerhaft, User-Scope):
[Environment]::SetEnvironmentVariable("VAULTPILOT", "$env:USERPROFILE\Projects\VaultPilot", "User")

# In der aktuellen Sitzung verfügbar machen (oder PowerShell neu starten):
$env:VAULTPILOT = "$env:USERPROFILE\Projects\VaultPilot"
```

**Konvention:** Pfade nie hartkodieren. In Leitfäden, Notizen, Checklisten und Befehlen wird das Repository immer über `$env:VAULTPILOT` adressiert. Standardort ist `$env:USERPROFILE\Projects\VaultPilot`.

## 🎯 Ziel

Wissen strukturiert ablegen, vernetzen und dauerhaft pflegen – unterstützt und automatisiert durch einen KI-Agenten.

## 📅 Roadmap

- [x] Projekt-Konzept & Ziele (finalisiert am 2026-10-27, siehe `CONCEPT.md`)
- [x] Git/GitHub-Repository anlegen
- [x] Vault-Struktur (Ordner / Tags / Frontmatter)
- [x] Agenten-Workflow mit OpenCode definiert und getestet
- [x] Installation, Einführung, Wissensbasis-Aufbau, Obsidian-Auswertung (abgeschlossen 2026-10-27)
- [ ] Pilotdurchlauf des Kurses mit Teilnehmern

## 🔭 Nächste Schritte

- [ ] Pilotdurchlauf des Kurses mit echten Teilnehmern
- [ ] Erfahrungswerte aus dem Piloten zurück in die Materialien (Kurs-Iteration)

## Status

✅ Projekt abgeschlossen (alle Erfolgskriterien K1–K6, alle Meilensteine M1–M4 – Details: `Abschlussbericht.md`) · bereit für Pilotdurchlauf
