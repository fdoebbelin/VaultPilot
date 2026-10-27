# VaultPilot

**VaultPilot** – Dein KI-Agent für dein zweites Gehirn.

## Überblick

Ein Kursprojekt zur Arbeit mit **agentischer KI** am Beispiel von **OpenCode**. Der Fokus liegt auf dem **Aufbau und der Verwaltung eines Obsidian Vaults** zum **Wissensmanagement**.

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

- [x] Projekt-Konzept & Ziele
- [x] Git/GitHub-Repository anlegen
- [ ] Vault-Struktur (Ordner / Tags / Frontmatter)
- [x] Agenten-Workflow mit OpenCode definieren
- [ ] Implementierung & Tests
- [x] Dokumentation & Abschlussbericht

## 🔭 Nächste Schritte

- [ ] GitHub-Repository initialisieren
- [ ] Umsetzung: Installation, Einführung, Wissensbasis-Aufbau

## Status

🚧 Projekt in Umsetzung
