# Das adaptive Wissensmodell — Health Backlog

## Das Problem ohne dieses System

Ein Gesundheits-Tagebuch das einfach wächst wird mit der Zeit unbrauchbar.
Nach einem Jahr: 80 Dateien, die Hälfte überholt, der KI-Kontext
wird riesig und unscharf. Was zählt gerade wirklich?

Das adaptive Wissensmodell löst das:
**Aktuelles bleibt vorne. Gelöstes wandert nach hinten. Nichts geht verloren.**

---

## Die drei Zonen

```
┌─────────────────────────────────────────────────────────┐
│  ZONE 1 — AKTIV                                         │
│  Was jetzt gerade relevant ist                          │
│  Lädt automatisch in jeden KI-Chat                      │
│                                                         │
│  • Offene Probleme                                      │
│  • Laufende Maßnahmen                                   │
│  • Beobachtungsthemen                                   │
└─────────────────────────────┬───────────────────────────┘
                              │ automatisch wenn gelöst
                              ▼
┌─────────────────────────────────────────────────────────┐
│  ZONE 2 — ZUSAMMENFASSUNG                               │
│  Die Essenz eines abgeschlossenen Themas                │
│  Kompakt, für schnellen Überblick                       │
│                                                         │
│  • Was war das Problem?                                 │
│  • Was hat geholfen?                                    │
│  • Was sollte man im Auge behalten?                     │
└─────────────────────────────┬───────────────────────────┘
                              │ verlinkt auf
                              ▼
┌─────────────────────────────────────────────────────────┐
│  ZONE 3 — VERLAUFSARCHIV                                │
│  Der vollständige Verlauf, nachvollziehbar              │
│  Wird nur geladen wenn man gezielt sucht                │
│                                                         │
│  • Alle Einträge chronologisch                          │
│  • Alle Messwerte                                       │
│  • Alle Gesprächs-Zusammenfassungen                     │
└─────────────────────────────────────────────────────────┘
```

---

## Die Status-Zustände

Jedes Gesundheitsthema hat einen Status der seinen Ort bestimmt:

| Status | Symbol | Bedeutung | Zone |
|--------|--------|-----------|------|
| **Offen** | 🔴 | Problem erkannt, Maßnahme noch nicht gestartet | Aktiv |
| **In Bearbeitung** | 🟡 | Maßnahme läuft, Ergebnis ausstehend | Aktiv |
| **Beobachten** | 🔵 | Verbessert, aber nächste Messung abwarten | Aktiv |
| **Gelöst** | ✅ | Problem behoben, stabil | Zusammenfassung |
| **Chronisch** | ♾️ | Dauerhaftes Thema, regelmäßige Kontrolle | Aktiv (kompakt) |
| **Kein Effekt** | ⬜ | Maßnahme hat nicht geholfen — wichtig zu wissen | Zusammenfassung |
| **Abgewartet** | 🕐 | Bewusst zurückgestellt | Aktiv (niedrig priorisiert) |

---

## Das Vitamin-D-Beispiel — vollständiger Lebenszyklus

### Phase 1 — Problem erkannt 🔴 OFFEN
```markdown
# Vitamin D — Mangel
Status: 🔴 Offen
Erstellt: 2026-01-15
Nächste Aktion: Supplementierung beginnen

## Messung
25-OH-Vitamin-D: 18 ng/ml (Referenz: 40-60)
→ Deutlicher Mangel

## Offene Fragen
- [ ] Welche Dosierung ist sinnvoll?
- [ ] Mit K2 kombinieren?
- [ ] Wann Kontrollmessung?
```

### Phase 2 — Maßnahme läuft 🟡 IN BEARBEITUNG
```markdown
# Vitamin D — Mangel
Status: 🟡 In Bearbeitung
Aktualisiert: 2026-01-20

## Laufende Maßnahme
Vitamin D3: 4.000 IE täglich + K2 200 mcg
Beginn: 2026-01-20
Kontrollmessung geplant: 2026-04-20 (3 Monate)

## Bisherige Messung
2026-01-15: 18 ng/ml 🔴
```

### Phase 3 — Abwarten nach Messung 🔵 BEOBACHTEN
```markdown
# Vitamin D — Mangel
Status: 🔵 Beobachten
Aktualisiert: 2026-04-22

## Verlauf
2026-01-15: 18 ng/ml 🔴 (Mangel)
2026-04-20: 52 ng/ml ✅ (Zielbereich erreicht)

## Aktuelle Maßnahme
Erhaltungsdosis: 2.000 IE täglich
Nächste Kontrolle: Oktober 2026 (nach Sommer)
```

### Phase 4 — Stabil gelöst ✅ → WANDERT IN ZUSAMMENFASSUNG
```markdown
# Vitamin D — gelöst ✅
Status: Gelöst | Archiviert: 2026-11-01

## Kurzfassung
Deutlicher Mangel (18 ng/ml) durch 3 Monate
Supplementierung (4.000 IE D3 + K2) behoben.
Stabil bei Erhaltungsdosis 2.000 IE.

## Was funktioniert hat
D3 4.000 IE + K2 200 mcg → Zielwert in 3 Monaten

## Im Auge behalten
Winterhalbjahr: tendenziell absinkend
Jährliche Kontrolle Oktober empfohlen

→ Vollständiger Verlauf: [Archiv/Vitamin-D-2026.md]
```

---

## Was die KI automatisch erledigt

### Themen zusammenführen
Wenn du über mehrere Gespräche hinweg über dasselbe Thema sprichst,
erkennt das System den Zusammenhang und pflegt eine einzige Datei —
statt viele unverbundene Einträge anzulegen.

### Status-Vorschläge
Nach einer neuen Messung schlägt die KI vor:
> *„Dein Vitamin-D-Wert ist jetzt im Zielbereich. Soll ich das Thema
>   auf 'Beobachten' setzen und die Dosierung aktualisieren?"*

Du bestätigst — oder korrigierst. Die KI entscheidet nie alleine
über Statuswechsel.

### Automatisches Archivieren
Wenn ein Thema seit 6 Monaten den Status "Gelöst" hat
und keine neuen Messungen zeigen, schlägt das System vor
es vollständig zu archivieren. Die Zusammenfassung bleibt,
der Verlauf wandert ins Archiv.

### Kontext-Optimierung
Beim Start eines neuen Chats lädt das System:
- ✅ Alle **Aktiv**-Dateien (vollständig)
- ✅ Alle **Zusammenfassungen** (kompakt, 1 Absatz)
- ❌ Archive (nur auf Nachfrage)

So bleibt der Kontext klein und scharf — auch nach Jahren.

---

## Ordnerstruktur auf dem Pi

```
healthledger/
└── backlog/
    ├── aktiv/                    ← lädt automatisch in KI-Chat
    │   ├── blutdruck.md          🟡 In Bearbeitung
    │   ├── schlaf.md             🔴 Offen
    │   └── hashimoto.md          ♾️ Chronisch
    │
    ├── zusammenfassungen/        ← kompakte Übersicht, auch im Chat
    │   ├── vitamin-d.md          ✅ Gelöst 2026-11
    │   ├── eisenmangel.md        ✅ Gelöst 2026-08
    │   └── rueckenschmerz.md    ⬜ Kein Effekt (Physiotherapie)
    │
    └── archiv/                   ← nur auf gezielten Abruf
        ├── vitamin-d-verlauf/
        │   ├── 2026-01-15.md
        │   ├── 2026-04-20.md
        │   └── 2026-10-15.md
        └── eisenmangel-verlauf/
            └── ...
```

---

## Das Tagebuch — chronologische Ansicht

Parallel zur thematischen Struktur gibt es eine **Tagebuch-Ansicht**:
alle Einträge chronologisch, egal zu welchem Thema.

```
2026-10-15  Vitamin D Kontrolle → 58 ng/ml, stabil ✅
2026-10-12  Blutdruck morgens erhöht, Gespräch gestartet 🔴
2026-09-30  Hashimoto — TSH Kontrolle, unverändert ♾️
2026-08-20  Eisen — Ferritin 45 ng/ml, Ziel erreicht ✅
...
```

So siehst du auf einen Blick: Was ist in letzter Zeit passiert?
Und das thematische System sagt: Was ist gerade relevant?

---

## Chronische Erkrankungen — Sonderfall ♾️

Themen wie Hashimoto, Diabetes oder Bluthochdruck werden nie
wirklich "gelöst" — sie bleiben dauerhaft relevant, aber
die Dringlichkeit wechselt.

Für chronische Themen gibt es eine **kompakte Dauerkarte**
die immer im Kontext bleibt — aber schlank ist:

```markdown
# Hashimoto ♾️ Chronisch
TSH zuletzt: 2,4 mU/l (2026-10-01) — stabil
Medikation: Levothyroxin 75 mcg morgens nüchtern
Nächste Kontrolle: April 2027
Aktuelle Besonderheiten: keine
→ Vollständiger Verlauf: [archiv/hashimoto/]
```

Nur wenn etwas aus dem Ruder läuft wechselt der Status
temporär auf 🟡 oder 🔴 — und kehrt nach Stabilisierung
wieder zu ♾️ zurück.
