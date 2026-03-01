# Vision & Geschäftsmodell

## Das Problem

Gesundheitsdaten sind heute fragmentiert: Apple Health, Arzt-Apps, Labore, Krankenkassen.
Alles bei Dritten. Kein Überblick. Keine Kontrolle.

HealthLedger gibt dir die Kontrolle zurück. Lokal. Privat. Open Source.

## Kernprinzip: Lokale Datensouveränität

**Alle persönlichen Daten bleiben verschlüsselt auf deinem Pi.**
Der Server (optional, für KI) ist Zero-Knowledge — er sieht keine Gesundheitsdaten.

## Automatisierte Entwicklung durch KI-Agenten

### Workflow
1. Nutzer schreibt Feature Request (GitHub Discussions)
2. Community voted + optionale Spende als Boost
3. KI-Agenten analysieren, implementieren, testen
4. PR wird erstellt → Maintainer Review → Merge
5. Spender erhalten Beta-Zugang zum Testen
6. Feedback wird automatisch eingearbeitet

## Finanzmodell

### Spendenbasiert — kein Abo-Zwang

| Spende | Zugang |
|--------|--------|
| €0 | Core-Funktionen, Self-hosted, kein KI-Server |
| €3/Mo | KI-Server-Nutzung + Feature Requests |
| €25/Jahr | KI-Server-Nutzung + Feature Requests |
| €10-50 | Feature Wunsch (direkte Priorisierung) |

### Anonyme Zahlung
- Crypto (Bitcoin, Monero) oder PayPal
- Token-System: Spende → anonymer Zugangstoken
- Keine Verbindung zwischen Zahlung und Identität
- Finanzen transparent und öffentlich einsehbar

### Server-Transparenz
- Server-Code vollständig open source
- Zero-Knowledge: Daten nur im RAM, sofort gelöscht
- Regelmäßige Community-Audits
- Monatliche Transparenzberichte

### Break-Even
~35 monatliche KI-Abos decken Serverkosten (Hetzner ~€20/Mo + Claude API ~€50/Mo)

## Supplement & Peptid Module (v1.2)

### Supplement-Verwaltung
- ~1000 gängige Supplements in Datenbank
- Wechselwirkungscheck mit Medikamenten
- Laborwert-basierte Empfehlungen
- Timing-Optimierung (Magnesium abends etc.)
- Stack-Builder

### Peptid-Rechner
- BPC-157, TB-500, GHK-Cu, Epithalon etc.
- Dosierungsrechner (nach KG)
- Zyklusplaner mit Pause-Empfehlungen
- Disclaimer: Research purposes only

### KI-Laboranalyse
- Werte in Kontext setzen (Alter, Geschlecht)
- Trends über Zeit erkennen
- Immer mit: Kein Arzt-Ersatz Disclaimer

## Differenzierung

| | HealthLedger | Apple Health | Kommerzielle EHR |
|--|--|--|--|
| Lokal/Privat | ✅ | ❌ | ❌ |
| Open Source | ✅ | ❌ | ❌ |
| Zero-Knowledge Server | ✅ | ❌ | ❌ |
| Anon. Spenden | ✅ | n/a | ❌ |
| KI-Analyse | ✅ | Begrenzt | ✅ teuer |
| Supplements/Peptide | ✅ | ❌ | ❌ |
| Kostenlos Core | ✅ | ✅ | ❌ |
| Familie | ✅ | Begrenzt | ❌ |

→ Details: [PRIVACY_MODEL.md](./PRIVACY_MODEL.md)
