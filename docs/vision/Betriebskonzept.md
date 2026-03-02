# Betriebskonzept — Pi Agent als autonomes Produkt

*Vision für den Betrieb mit 20–50 Kunden | Stand: März 2026*

---

## Die Ausgangslage

Pi Agent läuft heute auf einem Raspberry Pi 5 im Heimnetz.
Das funktioniert für die Familie — aber nicht für externe Kunden.

Wer Pi Agent für 20–50 Kunden betreiben will, braucht:
- Eine stabile, immer erreichbare Infrastruktur
- Einen lokalen KI-Server der große Modelle ausführt
- Einen autonomen Betrieb ohne manuellen Eingriff jeden Tag
- Datenschutz der deutschen und europäischen Anforderungen genügt

Dieses Dokument beschreibt den geplanten Weg dorthin.

---

## Was heute schon läuft

Der Betreiber hat bereits eine ausgewachsene KI-Infrastruktur zu Hause:

```
AI-NAS (Zuhause)
├── MSI RTX 5090 SUPRIM (24 GB VRAM)
├── AMD Ryzen 9 5950X
├── 128 GB ECC RAM
├── TrueNAS SCALE + Ubuntu AI-VM
└── Ollama mit: qwen2.5:32b, qwen3:32b, GLM-4-Flash, Qwen2.5-VL

Raspberry Pi 5 (PiAgent)
├── Alle 4 Pi Agent Module live
├── FastAPI + SQLite + FIDO2/YubiKey
└── Caddy HTTPS, Docker
```

Die Rechenpower ist vorhanden. Was fehlt, ist die Brücke nach außen:
ein dediziertes Gerät das als öffentlicher Eingang dient, stabil läuft
und den autonomen Betrieb koordiniert.

---

## Die Entscheidung: Mac mini statt Mietserver

### Warum kein Mietserver?

Ein Mietserver bei Hetzner oder ähnlichen Anbietern klingt einfach —
ist aber für Pi Agent aus einem grundlegenden Grund problematisch:

**Kein Mietserver kann lokale KI-Modelle sinnvoll ausführen.**

| Mietserver | Monatlich | Problem |
|-----------|-----------|---------|
| Hetzner CX42 (16 GB RAM) | ~20 €/Mo | Kein Platz für 32B-Modelle |
| Hetzner Dedicated 64 GB | ~150 €/Mo | Teuer, kein GPU |
| Hetzner GPU-Server | ab ~184 €/Mo | Zu teuer, Daten in fremder Hand |

Über 5 Jahre kostet ein tauglicher Mietserver ~9.000 €.
Und das größte Problem: **Die Gesundheitsdaten der Kunden liegen auf fremden Servern** —
ein K.O.-Kriterium für ein Produkt das auf Datenschutz und Vertrauen aufgebaut ist.

### Warum Mac mini?

Der Mac mini M-Series ist durch seine Unified-Memory-Architektur
für lokale KI-Modelle besser geeignet als jeder vergleichbar günstige PC:

- Idle-Verbrauch: **3–4 Watt** — läuft 24/7 für ~50 €/Jahr Strom
- KI-Last: 20–40 Watt — auch bei dauerhafter Nutzung sparsam
- Kein Lärm, kein Lüfter der stört, kein Ausfallrisiko durch Überhitzung
- macOS läuft stabil rund um die Uhr ohne manuelle Eingriffe
- Ollama läuft nativ auf Apple Silicon — schneller als auf Linux-Servern
- Kosten über 5 Jahre: **~2.100 €** (Kauf + Strom)

**Einsparung gegenüber Mietserver über 5 Jahre: ~6.900 €**

### Das geplante Gerät

**Mac mini M5 Pro — 64 GB Unified Memory / 1 TB SSD**

> ⏳ **Kaufentscheidung zurückgestellt bis M5 Pro verfügbar**
> Apple hat M5 und M5 Pro Mac mini für 2026 angekündigt (Frühling oder WWDC Juni 2026).
> Der M5-Chip bringt ~45% mehr GPU-Leistung und 3,5× schnellere KI-Tasks
> gegenüber M4 — bei gleichem Preis. Das Warten lohnt sich.

Warum 64 GB und nicht 48 GB?

Der Betrieb mehrerer autonomer Agenten parallel erfordert mehr RAM
als einfaches Web-Hosting. Jeder Agent mit seinem Kontext und Modell
braucht 14–20 GB. RAM ist beim Mac mini **nicht nachrüstbar** —
einmal gekauft, für die nächsten 5+ Jahre. Daher: großzügig wählen.

```
64 GB Verteilung im Vollbetrieb:
  macOS + System ................  8 GB
  4× FastAPI Apps (PiAgent) ....  2 GB
  OpenClaw Gateway + Agenten ...  3 GB
  Schnelle Routing-Modelle (7B).  8 GB
  Schwere Modelle (14B lokal) ..  16 GB
  KV-Cache (64K Kontext) .......  8 GB
  Puffer ...........................9 GB
  ─────────────────────────────────────
  Gesamt ......................... 54 GB ✅ (10 GB Reserve)
```

---

## Die Architektur

```
                        ┌─────────────────────────────────────┐
                        │     ÖFFENTLICHES INTERNET           │
                        │  20–50 Kunden, Browser, Apps        │
                        └──────────────┬──────────────────────┘
                                       │ HTTPS
                        ┌──────────────▼──────────────────────┐
                        │     MAC MINI M5 PRO 64 GB           │
                        │     "Orchestrator & Eingang"        │
                        │                                     │
                        │  FastAPI (4 PiAgent Module)         │
                        │  OpenClaw Gateway (Agenten-Team)    │
                        │  Caddy HTTPS Reverse Proxy          │
                        │  Ollama (7B–14B Modelle, schnell)   │
                        └──────────────┬──────────────────────┘
                                       │ LAN / Tailscale
                        ┌──────────────▼──────────────────────┐
                        │     AI-NAS / RTX 5090               │
                        │     "Gehirn für schwere Aufgaben"   │
                        │                                     │
                        │  Qwen2.5:32b, Qwen3:32b             │
                        │  Qwen2.5-VL (Vision/OCR)            │
                        │  GLM-4-Flash                        │
                        └──────────────┬──────────────────────┘
                                       │ bei Überlast
                        ┌──────────────▼──────────────────────┐
                        │     MIET-GPU (Runpod / Vast.ai)     │
                        │     "Notfall-Burst-Kapazität"       │
                        │  ~0,20–0,50 €/Stunde, on-demand    │
                        └─────────────────────────────────────┘
```

**Wie die Lastverteilung funktioniert:**

Einfache Anfragen (Beihilfe-Chat, kurze Fragen) → Mac mini lokal, ~35 t/s
Dokument-OCR, Vision-Aufgaben → AI-NAS RTX 5090, kein Limit
Spitzenzeiten wenn viele Kunden gleichzeitig → Miet-GPU automatisch zugeschaltet

Der Mac mini entscheidet selbst wohin eine Anfrage geht — kein manueller Eingriff.

---

## Das autonome Agenten-Team

Der Betrieb läuft nicht mit einer Person die alles überwacht.
Ein Team aus autonomen Agenten übernimmt die Routineaufgaben:

### 🤖 Support-Agent
Antwortet auf Kundenfragen über WhatsApp, Telegram oder E-Mail.
Kennt alle Pi Agent Module, die FAQ, bekannte Probleme.
Eskaliert an den Betreiber wenn er nicht weiterkommt.

### 📊 Buchhaltungs-Agent
Überwacht Token-Guthaben, verarbeitet Zahlungseingänge,
sendet Quittungen, erstellt monatliche Übersichten.
Schlägt Alarm bei ungewöhnlichen Mustern.

### 📣 Marketing-Agent
Beobachtet relevante Foren, Communities, Social Media —
und beteiligt sich dort hilfreich (kein Spam, kein Aufdrängen).
Sammelt Feedback und Feature-Wünsche aus öffentlichen Gesprächen.

### 🔧 Feature-Request-Agent
Nimmt Wünsche von Kunden entgegen, priorisiert sie nach Token-Voting,
erstellt strukturierte GitHub Issues und bereitet Implementierungspläne vor.

### ⚡ Infrastruktur-Agent
Überwacht Auslastung von Mac mini und AI-NAS.
Schaltet Miet-GPU automatisch zu wenn nötig.
Startet hängende Services neu, sendet Alerts bei Problemen.

**Technologie:** OpenClaw (oder vergleichbares Framework)
OpenClaw verbindet Messaging-Apps direkt mit dem Agenten-System —
ein Kunde schreibt auf Telegram, der Support-Agent antwortet,
ohne dass eine Person eingreifen muss.

---

## Datenschutz und Compliance

Pi Agent ist von Anfang an für deutschen und europäischen Datenschutz gebaut.
Das Betriebskonzept setzt das konsequent fort:

**Kein Datum verlässt die eigene Infrastruktur:**
- Kundendaten: Mac mini + NAS, beide in Deutschland, beide physisch beim Betreiber
- KI-Verarbeitung: lokal (Mac mini oder AI-NAS), nie über externe APIs
- Ausnahme: Miet-GPU bei Burst — **nur für anonymisierte, nicht-personenbezogene Aufgaben**

**Authentifizierung:** FIDO2/YubiKey und Passkey, kein Passwort-Login
**Verschlüsselung:** SQLCipher für Datenbanken, HTTPS für alle Verbindungen
**Token-System:** anonym über Monero/Bitcoin, kein KYC nötig

Das ist der entscheidende Unterschied zu Cloud-Alternativen:
Kein Anbieter außer dem Betreiber selbst hat je Zugriff auf Kundendaten.

---

## Finanzierung und Preismodell

### Für Kunden: Token-System

Kunden kaufen Guthaben — kein Abo, kein Verfallsdatum, anonym zahlbar.

| Paket | Preis | Token | Für was |
|-------|-------|-------|---------|
| Einsteiger | 5 € | 500 | ~15 Beihilfe-Anträge |
| Standard | 10 € | 1.100 | ~35 Anträge, 70 Chats |
| Unterstützer | 25 € | 3.000 | Jahresvorrat für eine Familie |
| Förderer | 50 € | 7.000 | Jahresvorrat + Feature-Voting |

Lokale Nutzung (eigener Pi zu Hause) bleibt dauerhaft kostenlos.
Das Token-System gilt nur für die Server-Infrastruktur.

### Kostendeckung für den Betreiber

```
Laufende Kosten pro Monat:
  Strom (Mac mini + AI-NAS) .....  ~15 €
  Domain, SSL, Monitoring .......   5 €
  Gelegentliche Miet-GPU ........  ~10 €
  Backup-Speicher ................  5 €
  ────────────────────────────────────
  Gesamt .........................  ~35 €/Monat

Break-Even bei Token-Verkauf:
  35 € / (10 €/Paket × 0,9 Marge) = ~4 zahlende Kunden/Monat
  Ab ~10 aktiven Kunden: profitabel
```

---

## Zeitplan

### Phase 1 — Vorbereitung (März–Juni 2026)
- Pi Agent läuft stabil auf dem Raspberry Pi
- Alle 4 Module getestet und dokumentiert
- Token-System implementiert
- OpenClaw-Agenten konfiguriert und getestet

### Phase 2 — Hardware-Entscheidung (Juni 2026)
- Apple WWDC abwarten (M5 Pro Mac mini Ankündigung erwartet)
- Mac mini M5 Pro 64 GB bestellen
- Hybrid-Architektur aufbauen (Mac mini ↔ AI-NAS)

### Phase 3 — Beta-Betrieb (Sommer 2026)
- Erste 5–10 Beta-Kunden onboarden
- Agenten-Team im echten Betrieb kalibrieren
- Feedback-Loop über Feature-Request-Agent etablieren

### Phase 4 — Vollbetrieb (Herbst 2026)
- 20–50 Kunden
- Agenten laufen autonom
- Betreiber kümmert sich nur noch um neue Features, nicht um Betrieb

---

## Was dieses Konzept nicht ist

Ein klassisches SaaS-Startup mit Venture Capital, Wachstumsdruck
und dem Geschäftsmodell "Daten gegen Dienst".

Pi Agent ist ein kleines, solides Werkzeug für Menschen die ihre
Daten selbst kontrollieren wollen — gebaut von jemandem der das
selbst nutzt, und angeboten für andere die dasselbe wollen.

Der Betrieb soll sich selbst tragen. Nicht mehr, nicht weniger.
Wenn 50 Kunden das Produkt nützlich genug finden um Token zu kaufen,
ist das ein Erfolg. Wenn es nur 20 sind, auch.

---

## Verwandte Dokumente

- [Das Gerät](./Das-Geraet.md) — Raspberry Pi für Einsteiger
- [KI-Architektur](./KI-Architektur.md) — Basis- und Premium-Modell
- [Datenschutz](./Datenschutz.md) — Privacy-Modell im Detail
- [Token-Finanzierungsmodell](./Token-Finanzierungsmodell.md) — Zwei-Seed-Anonymität
- [Roadmap](./Roadmap.md) — Was als nächstes kommt

---

*Dieses Dokument beschreibt den geplanten Betrieb, nicht den aktuellen Stand.*
*Alle Angaben zu Preisen und Hardware gelten Stand März 2026.*
