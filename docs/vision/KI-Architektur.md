# KI-Architektur — Basis & Premium

HealthLedger nutzt zwei KI-Modelle mit klar getrennten Aufgaben.
Jedes ist für seine Aufgabe optimiert — eines kostenlos und lokal,
eines leistungsstark und optional.

---

## Das Basis-Modell — Augen des Systems

### Was es tut
Das Basis-Modell ist darauf spezialisiert, **Fotos zu erkennen und auszulesen**.
Es läuft direkt auf deinem Pi — ohne Internet, ohne Kosten, ohne Verzögerung.

### Was es erkennt

| Foto | Was erkannt wird |
|------|-----------------|
| Arztbrief | Diagnose, Datum, Arzt, Empfehlungen |
| Laborzettel | Alle Werte mit Einheiten und Referenzbereichen |
| Rezept | Medikament, Dosierung, Einnahmehinweise |
| Blutdruckmessgerät | Systolisch, diastolisch, Puls vom Display |
| Blutzuckermessgerät | Wert, Uhrzeit |
| Medikamentenpackung | Name, Wirkstoff, Dosierung |
| Beihilfe-Rechnung | GOÄ-Ziffern, Betrag, Behandler, Datum |

### Wie es funktioniert
```
Du fotografierst ein Dokument
         ↓
Basis-Modell läuft lokal auf dem Pi
         ↓
Erkennt Text, Zahlen, Struktur
         ↓
Daten werden in die Datenbank übernommen
         ↓
Original-Foto bleibt archiviert
```

Dokumenten scannen passiert täglich und oft spontan —
das darf keine Kosten verursachen und darf nicht
von einer Internetverbindung abhängen.

---

## Das Premium-Modell — Gesprächspartner & Denker

### Was es tut
Das Premium-Modell führt echte Gespräche über Gesundheitsthemen.
Es kennt Studien, versteht Zusammenhänge, gibt durchdachte Antworten —
und es **lernt dich kennen** durch den Health Backlog.

### Was es kann

> *„Mein Ferritin ist zum dritten Mal gesunken. Was könnte das bedeuten
>   und welche Fragen sollte ich meinem Arzt stellen?"*

> *„Erkläre mir diesen Arztbrief — besonders was die Empfehlung
>   zur weiteren Abklärung bedeutet."*

> *„Welche Studien gibt es zu meiner Diagnose und integrativer Medizin?"*

Das Modell kennt deine gespeicherten Daten — Diagnosen, Medikamente,
Laborwerte — und gibt Antworten die zu dir passen, nicht generische.
Antworten werden mit echten Quellen belegt, immer mit Angabe
wie belastbar die Information ist.

### Wo es läuft
- **Option A — Eigene starke GPU**: Lokal, kostenlos, maximale Privatsphäre
- **Option B — HealthLedger Server**: Schnell, verbraucht Token,
  Zero-Knowledge (RAM only, sofort gelöscht)

---

## Der Health Backlog — dein wachsendes Gesundheitsgedächtnis

Nach jedem bedeutsamen Gespräch entsteht automatisch eine
strukturierte Datei auf deinem Pi. Mit der Zeit entsteht eine
persönliche Wissensbasis — aber eine die **nicht einfach wächst
und unhandlich wird**.

Das System unterscheidet automatisch:
- Was ist gerade aktuell und relevant?
- Was ist gelöst und kann kompakt archiviert werden?
- Was ist chronisch und bleibt dauerhaft im Blick?

→ **[Wie das Backlog-System funktioniert](./Health-Backlog-System)**

---

## Token-Verbrauch

| Aktion | Modell | Token |
|--------|--------|-------|
| Foto scannen | Basis | 0 — kostenlos |
| Einfache Frage | Basis (lokal) | 0 — kostenlos |
| Tiefes Gespräch (Server) | Premium | 10 / Nachricht |
| Dokument vollständig analysieren | Premium | 25 |
| Backlog-Eintrag erstellen/aktualisieren | Premium | 10 |
| Studie abrufen & zusammenfassen | Premium | 20 |

---

## Für Nutzer mit eigener GPU

Wer einen leistungsstarken Computer oder ein NAS mit Grafikkarte hat,
kann das Premium-Modell vollständig lokal betreiben —
keine Token nötig, noch mehr Privatsphäre.

Empfohlene Hardware: NVIDIA RTX 3060 oder besser.
Fertig-Konfigurationspaket verfügbar *(geplant)*.

→ [Dein HealthLedger-Gerät](./Das-Geraet)
