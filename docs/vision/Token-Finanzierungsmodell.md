# Token-Finanzierungsmodell

## Konzept: Prepaid-Token wie API-Credits

Analog zu Anthropic API Credits:
- Spende kauft Token-Guthaben
- KI-Features verbrauchen Token
- Mehr Nutzung = mehr Token nötig
- Kein Abo-Zwang, kein Verfallsdatum

```
Spende (€) → Token-Guthaben
                  ↓
         KI-Feature genutzt
                  ↓
         Token abgezogen
                  ↓
         Guthaben leer → neue Spende
```

## Token-Verbrauch (Beispiel)

| Feature | Token/Nutzung |
|---------|--------------|
| KI-Chat Nachricht (lokal) | 0 (kostenlos) |
| KI-Chat Nachricht (Server) | 5 |
| Dokument-Analyse | 20 |
| Laborwert-Interpretation | 15 |
| Studie abrufen + analysieren | 25 |
| Supplement-Check | 10 |
| Wechselwirkungscheck | 10 |

**Kaufen:**
- €5 → 500 Token
- €10 → 1.100 Token (+10% Bonus)
- €25 → 3.000 Token (+20% Bonus)
- €50 → 7.000 Token (+40% Bonus)

---

## Anonymitäts-Architektur: Zwei-Seed-Modell

### Das Problem
Zahlung und Datennutzung in einem System verbinden zu müssen
untergräbt Anonymität — Zahlungsanbieter kennt IP/Wallet,
Server kennt Nutzungsverhalten.

### Lösung: Strikte Trennung durch zwei Seeds

```
SEED A (Zahlungs-Seed)          SEED B (Nutzungs-Seed)
─────────────────────          ──────────────────────
Kennt: Guthaben                Kennt: Token-Balance
Kann: Guthaben aufladen        Kann: Features nutzen
Weiß nicht: wer nutzt          Weiß nicht: wer zahlt

         Verbindung: BLIND COMMITMENT
         (kryptographisch, nicht rückverfolgbar)
```

### Technische Umsetzung: Blind Token Transfer

**Konzept**: Ähnlich wie Blind Signatures (Chaum 1982)

```
1. SEED B generiert Token-Request (geblindet)
2. SEED A signiert Request OHNE Inhalt zu kennen
3. Server validiert Signatur → bucht Guthaben
4. Keine Verbindung A↔B auf Server-Seite möglich
5. Selbst bei kompromittiertem Server: keine Zuordnung
```

**Einfachere Variante (praktisch umsetzbar):**

```
Phase 1: Zahlung (SEED A)
─────────────────────────
User generiert SEED A (lokal, zufällig)
SEED A → Wallet-Adresse (Monero/Bitcoin)
User zahlt an Wallet
Server sieht: Zahlung eingegangen für Wallet X
Server generiert: Voucher-Hash (einmalig, zufällig)
Voucher-Hash → an User (via Onion/anonymem Kanal)
SEED A wird danach nicht mehr benötigt

Phase 2: Einlösen (SEED B)  
────────────────────────────
User generiert SEED B (lokal, zufällig, unabhängig)
User sendet: Voucher-Hash + SEED B public key
Server: Erstellt Token-Account für SEED B
Server: Invalidiert Voucher-Hash
Verbindung Zahlung↔Nutzung: NUR der Voucher-Hash
→ Nach Einlösung: Voucher gelöscht, keine Spur mehr

Phase 3: Nutzung (nur SEED B)
──────────────────────────────
Alle API-Calls: signiert mit SEED B
Server kennt nur: SEED B public key + Guthaben
Keine Verbindung zu Zahlung möglich
```

### Maximale Anonymität — Threat Model

| Angreifer | Was sie sehen | Was sie NICHT sehen |
|-----------|--------------|---------------------|
| Zahlungsanbieter (PayPal) | Zahlung an HealthLedger | Nutzungsverhalten, SEED B |
| Blockchain (Bitcoin) | Wallet-Adresse | Person, SEED B |
| Monero-Chain | Nichts (privacy coin) | Alles |
| HealthLedger Server | SEED B, Token-Verbrauch | Wer zahlt, echte Identität |
| Traffic-Analyse | Verbindung zu Server | Inhalt (TLS) |
| Kompromittierter Server | SEED B accounts + Guthaben | Zahlungsverbindung |

**Schwachstelle**: Voucher-Hash-Transfer
→ Mitigation: Transfer über Tor/I2P oder Out-of-Band (z.B. QR-Code)

---

## Implementierungsplan

### MVP (einfach, weniger anonym)
```
Zahlung → Monero-Wallet → manueller Voucher-Code → Token-Account
```
- Einfach zu implementieren
- Monero gibt ausreichend Anonymität
- Voucher-Code per E-Mail oder Display

### Full Privacy (komplex, maximal anonym)
```
Blind Signature Protocol + Tor-Integration
```
- Benötigt kryptographisches Know-how
- Empfehlung: Cashu oder Lightning Network als Basis nutzen

### Empfehlung: Cashu (Ecash-Protokoll)

**Cashu** ist ein Open-Source Ecash-Protokoll für Lightning/Bitcoin:
- Blind signatures eingebaut
- Bearer tokens (wie Bargeld digital)
- Mint kennt nur Gesamtvolumen, nicht wer was ausgibt
- Perfekt für unser Use-Case

```
User zahlt Lightning Invoice
→ erhält Cashu Token (blind, nicht rückverfolgbar)
→ löst Cashu Token beim HealthLedger Mint ein
→ erhält API-Guthaben auf SEED B
→ Mint kennt keine Verbindung
```

---

## Lokale Token-Verwaltung

Guthaben wird **lokal auf dem Pi** gespeichert — nicht nur auf dem Server.

```
Pi speichert (verschlüsselt):
  - SEED B (privater Schlüssel)
  - Lokale Token-Balance (Cache)
  - Nutzungshistorie (nur lokal)

Server speichert:
  - SEED B public key hash
  - Guthaben (autoritativ)
  - Nutzungslog (anonym, 30 Tage)
```

Vorteile:
- Offline-Nutzung mit lokalem Modell verbraucht keine Server-Token
- Transparenz: User sieht eigenen Verbrauch lokal
- Redundanz: Bei Server-Ausfall keine Datenverluste

---

## Zusammenfassung

```
EINFACH ERKLÄRT:

1. Du generierst zwei zufällige Schlüssel (Seeds) auf deinem Pi
2. Mit Seed A zahlst du anonym (Monero/Cashu/Bitcoin)
3. Du bekommst einen Einmal-Voucher
4. Mit Seed B löst du den Voucher ein → Guthaben
5. Seed A und Seed B kennen sich nicht
6. Der Server sieht nur Seed B und dein Guthaben
7. Niemand kann Zahlung und Nutzung verbinden

Selbst wenn HealthLedger kompromittiert wird:
Kein Angreifer kann herausfinden wer was gezahlt hat.
```
