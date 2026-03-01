# Privacy & Trust Model

## Grundprinzip: Zero-Knowledge Server

HealthLedger ist nach dem Prinzip gebaut: **Der Server weiß nichts. Der Pi weiß alles.**

```
┌─────────────────────┐         ┌──────────────────────┐
│   DEIN PI (lokal)   │         │   SERVER (optional)  │
│                     │         │                      │
│ ✅ Alle Gesundheits-│         │ ❌ Keine Gesundheits-│
│    daten            │         │    daten              │
│ ✅ Verschlüsselt    │         │ ✅ Nur Spenden-Token  │
│ ✅ Nur du hast Key  │         │ ✅ Nur während Verarb.│
│ ✅ Kein Cloud-Sync  │         │    dann alles gelöscht│
└─────────────────────┘         └──────────────────────┘
```

---

## Spenden-System: Anonym & Transparent

### Zahlungswege
- **Crypto**: Bitcoin, Monero (maximale Anonymität)
- **PayPal**: Optional, für Nutzer ohne Crypto
- **Ko-fi / GitHub Sponsors**: Für einfache Handhabung

### Wie Anonymität funktioniert
1. Spende wird geleistet (Crypto oder PayPal)
2. System generiert **Spenden-Token** (zufälliger Hash)
3. Token wird an Spender übermittelt
4. Token gibt Zugang zu Feature Requests + KI-Server
5. **Keine Verbindung** zwischen Token und echter Identität

```
Spender ──→ Zahlung ──→ System generiert Token
                              │
                              ▼
                    Token = Zugangsschlüssel
                    (anonym, nicht rückverfolgbar)
```

### Was getrackt wird (transparent, öffentlich)
- Gesamtbetrag pro Zeitraum
- Anzahl aktiver Abos
- Verteilung auf Entwicklung / Server / Reserve

### Was NICHT getrackt wird
- Wer gespendet hat
- Welcher Token zu welcher Person gehört
- Nutzungsverhalten auf dem Server

---

## Server-Mietmodell

### Prinzip: Spende = Server-Zugang

| Spende | Zugang | Laufzeit |
|--------|--------|----------|
| €3 | KI-Server + Feature Requests | 1 Monat |
| €25 | KI-Server + Feature Requests | 12 Monate |
| €50 | KI-Server + Priority Feature Requests | 12 Monate |
| €10-50 | Feature Wunsch Boost | Einmalig |

### Server-Transparenz
- Server-Code ist **vollständig open source** und auditierbar
- Alle Requests werden nur **im RAM** verarbeitet
- **Keine persistente Speicherung** von Nutzdaten
- Nach Verarbeitung: sofortiges Löschen
- Regelmäßige **Security Audits** (Community)
- Server-Logs: Nur Metadaten (Zeitstempel, Tokenhash), keine Inhalte

### Datenfluss KI-Server
```
Dein Pi ──[verschlüsselt]──→ Server
                                │
                                ▼
                         KI verarbeitet
                         (nur RAM, nie Disk)
                                │
                                ▼
                         Antwort zurück
                                │
                                ▼
                         RAM gecleart ✅
```

---

## Lokale Datensicherheit (Pi)

### Verschlüsselung
- Alle Gesundheitsdaten: **AES-256** verschlüsselt
- Schlüssel: Abgeleitet vom YubiKey / Passkey
- Backup-Verschlüsselung: Age-Encryption mit eigenem Schlüsselpaar
- SQLCipher für Datenbank (geplant v1.1)

### Zugang
- **FIDO2/WebAuthn**: YubiKey oder Passkey
- Notfallkarte: Auth-frei aber nur lesend (für Rettungskräfte)
- Familien-Rollen: Eigene Keys pro Person

### Was verlässt den Pi nie
- Rohdaten
- Dokumente
- Verschlüsselungsschlüssel
- Persönliche Identifikation

---

## Transparenz-Berichte

Monatlich veröffentlicht:
- Server-Kosten vs. Spendeneinnahmen
- Anzahl aktiver Token (anonym)
- Entwicklungsfortschritt
- Security-Incidents (falls vorhanden: sofortige Disclosure)

Format: Öffentliches Dashboard + GitHub-Report

---

## Trust-Architektur Zusammenfassung

```
VERTRAUEN BRAUCHST DU NUR DIR SELBST:

Dein Pi:
  ✅ Open Source — jede Zeile prüfbar
  ✅ Kein Cloud-Zwang
  ✅ Verschlüsselt
  ✅ Du hast den einzigen Key

Unser Server (optional):
  ✅ Open Source — jede Zeile prüfbar
  ✅ Zero-Knowledge — wir sehen keine Daten
  ✅ Spende = anonym
  ✅ Alles auditierbar
  ✅ Sofort-Löschung nach Verarbeitung

Spenden:
  ✅ Crypto möglich (Monero für max. Anonymität)
  ✅ Token-System — keine Identität nötig
  ✅ Finanzen öffentlich nachvollziehbar
```

---

*Wir bauen das System so, dass du uns nicht vertrauen musst — 
aber wenn du es tust, haben wir es verdient.*
