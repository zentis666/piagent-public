# Aktueller Stand — Was wir bereits haben

*Stand: Februar 2026 — Basis-Implementierung auf Raspberry Pi 5*

## ✅ Implementiert

### Backend (FastAPI, Python, ~950 Zeilen)
- REST API mit ~40 Endpoints
- SQLite Datenbank
- Ollama Integration für lokale KI (qwen2.5:32b)
- Audit-Log, Multi-User (Personen-Tabelle)

### Frontend (PWA, Vanilla JS)
- Progressive Web App — installierbar auf iOS/Android
- Dark Mode, responsive Design
- Bottom Navigation: Übersicht, Upload, Dokumente, Gesundheit, Notfall, KI-Hilfe

### Authentifizierung
- FIDO2/WebAuthn: YubiKey und iCloud Passkey
- HTTPS via Caddy Reverse Proxy (Port 8443, self-signed)
- JWT Sessions (8h), Setup-Mode für Ersteinrichtung

### Gesundheitsdaten
- Messwerte: Gewicht, Blutdruck, Puls, Temperatur, Blutzucker, SpO2, BMI, Körperfett
- Dokumente: PDF/Foto Upload mit KI-Extraktion
- Medikamente: Tracking, Dosierung, Einnahmezeiten
- Laborwerte: Freie Eingabe mit Einheiten

### Besondere Features
- **Notfallkarte**: Auth-freier Endpunkt für Rettungskräfte
- **Apple Health Import**: ZIP/XML, 10 Messtypen, iOS 16+ DTD-Fix, Deduplizierung
- **KI-Chat**: Lokal via Ollama, kontextbewusst
- **Familien-Support**: Mehrere Profile mit eigenem Zugang

### Infrastruktur
- Docker + docker-compose auf Raspberry Pi 5
- Caddy HTTPS Reverse Proxy
- NAS-Mount für Daten (/mnt/tank/family/healthledger/)

## 🔧 In Arbeit
- YubiKey Hardware-Login (Passkey läuft, YubiKey frisch zurückgesetzt)
- SQLCipher Datenbank-Verschlüsselung
- JWT_SECRET persistent (aktuell ephemer)
- Apple Health export.zip Test-Import

## 🗂️ Repos
- Referenzimplementierung: github.com/zentis666/healthledger-pi
- Dieses Konzept-Repo: github.com/zentis666/healthledger-open
