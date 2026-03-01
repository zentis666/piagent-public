# Das HealthLedger-Ökosystem

Auf den ersten Blick ist HealthLedger eine App für Gesundheitsdaten.
Aber es ist mehr — ein Ökosystem aus Werkzeugen, Community und Diensten
die alle zusammenspielen. Hier ein Überblick über das große Bild.

---

## Die Idee dahinter

Gesundheit ist ein Lebensbereich der bisher von vielen Einzellösungen
bedient wird: Diese App für Laborwerte, jene für Medikamente,
das Papierformular für Beihilfe, Google für Supplement-Fragen,
das Forum für Erfahrungen mit Erkrankungen.

HealthLedger bringt das zusammen — und macht daraus ein
zusammenhängendes System bei dem alles miteinander spricht.

---

## Die vier Säulen

```
┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│   DEIN GERÄT    │  │   KI-ASSISTENT  │  │   COMMUNITY     │  │   DIENSTE       │
│                 │  │                 │  │                 │  │                 │
│ Alle deine      │  │ Lokal auf dem   │  │ Wissen teilen   │  │ Beihilfe        │
│ Gesundheits-    │  │ Pi oder über    │  │ Erfahrungen     │  │ PKV             │
│ daten sicher    │  │ Server (anonym) │  │ bewerten        │  │ Supplements-DB  │
│ verschlüsselt   │  │                 │  │ Features wählen │  │ Studien-Chat    │
└─────────────────┘  └─────────────────┘  └─────────────────┘  └─────────────────┘
```

---

## Was alles zum Ökosystem gehört

### 🏠 Das Gerät — deine Datenzentrale
Der Raspberry Pi zu Hause ist die Grundlage.
Alle persönlichen Daten liegen hier — verschlüsselt, nur für dich.
Selbst gebaut oder als Fertig-Gerät.
→ [Dein HealthLedger-Gerät](./Das-Geraet)

### 🤖 Der KI-Assistent
Läuft auf deinem Pi für einfache Fragen (kostenlos, privat).
Für komplexere Anfragen (Studien analysieren, lange Dokumente)
optional über unseren Server — anonym, sofort gelöscht.
→ [Kosten & Token](./Kosten-und-Spenden)

### 🏥 Die Module
Jeder Lebensbereich hat sein eigenes Modul — alle teilen dieselben Daten:

| Modul | Was es tut |
|-------|-----------|
| **Dokumente** | Arztbriefe, Befunde scannen & verstehen |
| **Messwerte** | Blutdruck, Gewicht, Labor — alles im Verlauf |
| **Medikamente** | Übersicht, Dosierung, Erinnerungen |
| **Beihilfe** | Anträge automatisch ausfüllen |
| **PKV** | Rechnungen für private KV einreichen |
| **Supplements** | Was wann, Wechselwirkungen prüfen |
| **Laboranalyse** | Blutwerte verstehen und verfolgen |
| **Chronische Erkrankungen** | Verlauf, Therapie, Studien-Chat |
| **Notfallkarte** | Lebensrettende Infos ohne Login abrufbar |
| **Familien-Verwaltung** | Alle Familienmitglieder, jeder mit eigenem Zugang |

### 👥 Die Community
Nutzer die es wollen, teilen anonymisierte Erfahrungen.
Andere können abstimmen, kommentieren, davon profitieren.
Wissen entsteht von unten — nicht von oben verordnet.
→ [Gesundheits-Module](./Gesundheits-Module)

### 💰 Das Finanzierungsmodell
Keine Werbung. Keine Investoren. Keine Datenweitergabe.
Wer Wert bekommt, spendet freiwillig — anonym, per Crypto oder PayPal.
Spenden kaufen Token die KI-Features freischalten.
Wer mehr Geld spendet, kann Features priorisieren.
→ [Kosten & Spenden](./Kosten-und-Spenden)

### 🔧 Die Entwicklung
KI-Agenten setzen Feature-Wünsche automatisch um.
Der Code ist öffentlich — jeder kann prüfen was das System wirklich tut.
Maintainer prüfen und freigeben, die Community testet.
→ [Mitmachen](./Mitmachen)

---

## Wie alles zusammenhängt

```
Du fotografierst eine Arztrechnung
          ↓
Dokument-Modul liest sie aus
          ↓
Beihilfe-Modul befüllt automatisch den Antrag
          ↓
Medikamenten-Modul übernimmt neue Verschreibungen
          ↓
KI-Assistent erklärt was der Arzt diagnostiziert hat
          ↓
Disease-Management-Modul pflegt den Verlauf
          ↓
Community zeigt: andere mit dieser Diagnose berichten...
```

Ein Dokument hochladen — und das gesamte System wird klüger.

---

## Wer profitiert wovon

| Zielgruppe | Hauptnutzen |
|-----------|------------|
| **Beamte & Familien** | Beihilfe automatisiert, Zeit & Geld gespart |
| **Chronisch Kranke** | Verlauf dokumentiert, Studien verständlich |
| **Gesundheitsbewusste** | Supplements optimiert, Laborwerte verstanden |
| **Privacy-Nutzer** | Volle Kontrolle, kein Cloud-Zwang |
| **Biohacker** | Peptid-Rechner, Stack-Optimierung, Daten-Kontrolle |
| **Familien** | Alle Gesundheitsdaten zentral, Notfallkarte |

---

## Das große Bild

HealthLedger will nicht die eine App für alles sein.
Es will die **Infrastruktur** sein auf der Gesundheitssouveränität
aufgebaut wird — für Einzelpersonen, Familien, und irgendwann
vielleicht für kleine Arztpraxen die ihren Patienten etwas Besonderes
anbieten wollen.

Offen. Dezentral. Dem Nutzer gehörend.

> *„Wir bauen das System so, dass du uns nicht vertrauen musst —*
> *aber wenn du es tust, haben wir es verdient."*
