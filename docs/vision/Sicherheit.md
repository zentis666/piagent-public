# Sicherheit — Verschlüsselung & Authentifizierung

Gesundheitsdaten gehören zu den sensibelsten Informationen die es gibt.
Diese Seite erklärt konkret wie HealthLedger sie schützt —
ohne Fachbegriffe wo es geht, mit Erklärungen wo sie nötig sind.

---

## Der Grundsatz

**Sicherheit ist keine Option — sie ist eingebaut.**

HealthLedger wurde von Anfang an mit dem Gedanken entworfen:
Was passiert wenn jemand Böses Zugang zum Pi bekommt?
Was wenn der Server kompromittiert wird?
Was wenn jemand den Netzwerkverkehr abhört?

Die Antwort auf alle drei: Er findet nichts Verwertbares.

---

## Verschlüsselung — deine Daten sind unlesbar für alle außer dir

### Was Verschlüsselung bedeutet
Stell dir vor, deine Daten werden in eine Sprache übersetzt
die nur du lesen kannst — mit einem Schlüssel der nur auf
deinem Gerät existiert. Selbst wenn jemand die Dateien stiehlt,
sieht er nur unlesbaren Zeichensalat.

### Wie HealthLedger verschlüsselt

**Datenbank-Verschlüsselung (AES-256)**
Alle Gesundheitsdaten in der Datenbank sind mit dem stärksten
verfügbaren Standard verschlüsselt — demselben der von Banken,
Militär und Regierungen weltweit verwendet wird.

**Übertragungsverschlüsselung (HTTPS/TLS)**
Alle Verbindungen zu deinem Pi — egal ob aus dem Heimnetz
oder von unterwegs — laufen verschlüsselt.
Niemand kann den Datenverkehr abhören.

**Backup-Verschlüsselung**
Auch Sicherungskopien werden verschlüsselt gespeichert.
Ein gestohlenes Backup ist wertlos ohne deinen Schlüssel.

**Server: Nur im Arbeitsspeicher**
Wenn du den optionalen KI-Server nutzt, landen deine Daten
dort nie auf der Festplatte — nur im flüchtigen Arbeitsspeicher.
Nach der Antwort: automatisch gelöscht. Spurlos.

---

## Authentifizierung — wer kommt rein?

### Das Problem mit Passwörtern
Passwörter sind das schwächste Glied in der Sicherheitskette:
Zu einfach gewählt, wiederverwendet, durch Phishing gestohlen.
HealthLedger setzt auf modernere Methoden.

### Passkey — der neue Standard

Ein **Passkey** ist ein kryptographischer Schlüssel der auf deinem
Gerät gespeichert wird — im Chip deines iPhones, Macs oder
im Passwort-Manager.

Was das bedeutet:
- Kein Passwort das man vergessen oder stehlen kann
- Kein Phishing möglich (Passkey funktioniert nur auf der echten Seite)
- Entsperren mit Face ID, Touch ID oder Geräte-PIN
- Automatisch auf allen deinen Apple-Geräten verfügbar (iCloud Keychain)

### YubiKey — der Hardware-Sicherheitsschlüssel

Ein **YubiKey** ist ein kleiner USB-Stick der als physischer
Sicherheitsschlüssel dient. Du steckst ihn ein (oder hältst ihn ans
iPhone — NFC), tippst den goldenen Kontakt an — fertig, eingeloggt.

Was das besonders sicher macht:
- Der Schlüssel verlässt den YubiKey nie
- Selbst wenn jemand dein Passwort kennt — ohne den Stick kommt er nicht rein
- Funktioniert auch wenn dein Telefon gestohlen wurde

HealthLedger unterstützt beide Methoden — Passkey und YubiKey.
Du kannst auch beide kombinieren: YubiKey als Hauptzugang,
Passkey als Backup.

---

## Notfallkarte — Zugang ohne Login

Die Notfallkarte ist ein Spezialfall: Sie muss ohne Login
zugänglich sein — damit Sanitäter im Ernstfall sofort
Allergien und Medikamente sehen können.

**Wie das sicher ist:**
- Die Notfallkarte zeigt nur was du explizit dafür freigibst
- Keine anderen Daten sind zugänglich
- Der Link zur Notfallkarte ist ein langer zufälliger Code —
  praktisch unmöglich zu erraten
- Du kannst den Link jederzeit zurücksetzen

---

## Fernzugriff — sicher von unterwegs

Wenn du von unterwegs auf deinen Pi zugreifst (z.B. mit dem Handy
beim Arztbesuch), läuft das über einen verschlüsselten Tunnel
(Tailscale VPN).

Was das bedeutet:
- Dein Pi ist **nicht** direkt aus dem Internet erreichbar
- Nur Geräte die du explizit autorisiert hast, können sich verbinden
- Auch öffentliches WLAN ist kein Risiko

---

## Zusammenfassung — was ein Angreifer bräuchte

Um an deine Daten zu kommen, müsste jemand gleichzeitig:

1. ✅ Physischen Zugang zu deinem Pi zu Hause haben
2. ✅ Deinen Verschlüsselungsschlüssel kennen
3. ✅ Deinen YubiKey oder dein entsperrtes Gerät haben
4. ✅ Deinen Zugangscode knacken

Das ist in der Praxis nicht umsetzbar.

---

## Open Source als Sicherheitsmerkmal

Alle Sicherheitsmechanismen sind im öffentlichen Code einsehbar.
Sicherheitslücken können von jedem gefunden und gemeldet werden —
nicht erst wenn ein Angreifer sie ausnutzt.

> *„Security through obscurity"* — Sicherheit durch Geheimhaltung —
> ist keine echte Sicherheit. Offener Code der von vielen geprüft wird,
> ist sicherer als geschlossener Code den niemand prüfen kann.
