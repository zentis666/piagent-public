# Dein HealthLedger-Gerät

HealthLedger läuft auf einem kleinen Computer der bei dir zu Hause steht.
Er ist ungefähr so groß wie ein Taschenbuch, macht keinen Lärm,
verbraucht kaum Strom — und läuft einfach im Hintergrund.

---

## Was ist ein Raspberry Pi?

Ein Raspberry Pi ist ein vollwertiger kleiner Computer der für
solche Aufgaben gemacht wurde: immer an, immer verfügbar,
günstig im Betrieb.

Er kostet als Bausatz etwa **80–120 €** und verbraucht weniger Strom
als eine LED-Glühbirne (~5 Watt). Du schließt ihn ans Heimnetz an —
fertig. Von da an läuft HealthLedger rund um die Uhr.

Von außerhalb des Heimnetzes (z.B. unterwegs mit dem Handy)
erreichst du ihn sicher über einen verschlüsselten Tunnel —
ohne dass er dabei aus dem Internet erreichbar ist.

---

## Drei Wege zu deinem HealthLedger

### 🔧 Option 1 — Selbst bauen (für Technik-Interessierte)

Du kaufst die Teile selbst, folgst unserer Schritt-für-Schritt-Anleitung
und installierst HealthLedger mit einem einzigen Befehl.

**Was du brauchst:**

| Teil | Kosten |
|------|--------|
| Raspberry Pi 5 (4GB) | ~60 € |
| Netzteil (offiziell) | ~12 € |
| MicroSD-Karte (64GB) | ~12 € |
| Gehäuse (optional) | ~10 € |
| **Gesamt** | **~95 €** |

**Installation:**
```
1. SD-Karte mit dem Pi-Betriebssystem bespielen (Anleitung vorhanden)
2. Pi ans Netzwerk anschließen und starten
3. Einen einzigen Befehl im Browser eingeben
4. HealthLedger läuft — fertig
```

Die gesamte Einrichtung dauert etwa **30–45 Minuten**.
Du brauchst dafür kein technisches Vorwissen — nur die Bereitschaft
einer einfachen Anleitung zu folgen.

→ Zur Installationsanleitung *(coming soon)*

---

### 📦 Option 2 — Fertig-Gerät kaufen (Plug & Play)

Du bekommst ein fertig eingerichtetes Gerät — einschalten, ins Netzwerk
stecken, fertig. Keine Installation, keine Kommandozeile.

**Was enthalten ist:**
- Raspberry Pi 5 mit ausreichend Speicher
- HealthLedger vorinstalliert und konfiguriert
- Schutzhülle
- Netzteil
- Kurzanleitung auf Papier
- 1 Jahr E-Mail-Support

**Preis:** ca. **149–179 €** *(geplant)*

Das Fertig-Gerät wird entweder direkt über HealthLedger
oder über ausgewählte Partner angeboten.

→ Interesse am Fertig-Gerät? [Kontakt aufnehmen](./Mitmachen)

---

### ☁️ Option 3 — Cloud-Version (ohne eigenes Gerät)

Wer keinen eigenen Computer aufstellen möchte, kann HealthLedger
auch über einen gemieteten Server betreiben.

**Wichtig:** Dabei liegen die Daten nicht bei dir zu Hause,
sondern auf einem Server in einem deutschen Rechenzentrum.
Die Verschlüsselung bleibt bestehen — aber das Prinzip
„Daten nur bei dir" gilt dann nicht mehr vollständig.

Für viele ist das ein akzeptabler Kompromiss.
Für alle die maximale Kontrolle wollen, ist Option 1 oder 2 besser.

**Preis:** ca. **€5/Monat** für Hosting *(geplant)*

---

## Welche Option passt zu mir?

| Ich bin… | Empfehlung |
|----------|-----------|
| Technik-affin, spare gerne | Option 1 — Selbst bauen |
| Will es einfach, zahle lieber einmal mehr | Option 2 — Fertig-Gerät |
| Will gar kein Gerät zu Hause | Option 3 — Cloud |
| Beamter mit Familie, will Beihilfe automatisieren | Option 2 empfohlen |

---

## Wie viel Strom kostet der Pi?

Ein Raspberry Pi 5 verbraucht im Betrieb ca. 5 Watt.
Das sind bei Dauerbetrieb etwa **44 kWh pro Jahr** —
bei 30 Cent/kWh: **ca. 13 € Stromkosten pro Jahr**.

---

## Was passiert wenn der Pi ausfällt?

Alle Daten werden regelmäßig automatisch gesichert —
auf einen zweiten Speicherort den du selbst festlegst
(z.B. eine externe Festplatte oder ein NAS).
Wenn der Pi ausfällt, sind deine Daten nicht verloren.
Ein neuer Pi ist in 30 Minuten eingerichtet und wiederhergestellt.
