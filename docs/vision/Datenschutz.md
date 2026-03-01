# Datenschutz — Wer sieht meine Daten?

## Die kurze Antwort

**Nur du.**

Alle deine Gesundheitsdaten liegen verschlüsselt auf deinem eigenen Gerät.
Wir als Betreiber von HealthLedger sehen sie nicht. Können sie nicht sehen.
Das ist kein Versprechen — es ist Architektur.

---

## Wie das technisch funktioniert

### Dein Gerät ist die Zentrale
HealthLedger läuft auf einem kleinen Computer bei dir zu Hause —
einem Raspberry Pi oder einem NAS (Netzwerkspeicher).
Alle Daten liegen dort, verschlüsselt, nur für dich zugänglich.

```
DEIN GERÄT ZU HAUSE          INTERNET / CLOUD
─────────────────────         ───────────────────
✅ Alle Arztbriefe            ❌ Keine Gesundheitsdaten
✅ Alle Messwerte             ❌ Keine Dokumente
✅ Alle Medikamente           ❌ Keine Persönlichkeitsprofile
✅ Verschlüsselt              ✅ Nur anonyme Token-Infos
✅ Nur du hast den Schlüssel
```

### Was ist mit dem KI-Server?
Für erweiterte KI-Funktionen (z.B. Studie analysieren, komplexe Befunde)
kann optional unser Server genutzt werden. Dabei gilt:

- Die Daten werden **nur im Arbeitsspeicher** verarbeitet
- **Nie** auf Festplatte geschrieben
- **Sofort gelöscht** nach der Antwort
- Der Server sieht nur was du in die Frage schreibst — nicht deine gesamte Akte

Du kannst auch alles lokal laufen lassen — dann braucht kein Server involviert zu werden.

---

## Anonyme Nutzung

HealthLedger braucht keinen Account, keine E-Mail-Adresse, keinen Namen.

Stattdessen funktioniert es so:
1. Du erzeugst einen zufälligen Schlüssel auf deinem Gerät
2. Dieser Schlüssel ist deine Identität
3. Niemand außer dir kennt die Verbindung zwischen Schlüssel und Person

Für Token-Käufe (KI-Funktionen) gibt es sogar ein System mit
**zwei getrennten Schlüsseln** — einer für die Zahlung,
einer für die Nutzung. Beide kennen sich nicht.
Selbst wenn jemand die Zahlung sehen könnte:
er kann nie herausfinden, wer damit was genutzt hat.

---

## Was wir NICHT tun

- ❌ Deine Daten verkaufen
- ❌ Werbung schalten
- ❌ Daten an Versicherungen weitergeben
- ❌ Daten für KI-Training verwenden
- ❌ Profile über dich erstellen
- ❌ Dich tracken

---

## Warum du uns nicht einfach glauben musst

Der gesamte Code von HealthLedger ist öffentlich einsehbar.
Jeder Programmierer kann prüfen, was das System wirklich tut.
Wir können gar nicht unbemerkt lügen.

> *„Wir bauen das System so, dass du uns nicht vertrauen musst —*
> *aber wenn du es tust, haben wir es verdient."*

---

*Weiter lesen: [Kosten & Spenden →](./Kosten-und-Spenden)*
