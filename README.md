# Pausenplatz Lernspiele

Startseite für meine Lern-Apps. Die Kinder tippen auf ein Feld des Hüpfspiels und das Spiel öffnet sich.

## Aufbau

- `index.html`: der Pausenplatz (Startseite)
- `apps.js`: die Liste der Spiele, ein Eintrag pro Feld
- `apps/`: die Spiele selbst als HTML-Dateien

## Seite einschalten (einmalig)

1. Auf GitHub im Repo auf **Settings** gehen.
2. Links **Pages** wählen.
3. Bei **Source** «Deploy from a branch» wählen, Branch `main`, Ordner `/ (root)`, **Save**.
4. Nach ein bis zwei Minuten steht oben die Adresse der Seite,
   z.B. `https://benihonegger-source.github.io/LandingpageApps/`.

## Neue Version einer App

Die Datei im Ordner `apps` durch die neue Version ersetzen, **mit genau gleichem Namen**
(auf GitHub: Ordner `apps` öffnen → «Add file» → «Upload files»). Nach ein bis zwei Minuten ist sie online.
Sehen die Kinder noch die alte Version: Seite einmal neu laden.

## Neue App hinzufügen

1. Die HTML-Datei in den Ordner `apps` hochladen. Dateiname am besten ohne Leerzeichen und Umlaute,
   z.B. `rechentrainer-2.html`.
2. In `apps.js` einen Eintrag kopieren und anpassen (Komma zwischen den Einträgen nicht vergessen).
   Die Reihenfolge in der Liste ist die Reihenfolge der Felder.

## Lernstand-Code und Lehrerzimmer

Jede Lern-App mit Lernstand hat auf der Startseite den Knopf **«Lernstand-Code»**. Er zeigt einen QR-Code
mit dem aktuellen Lernstand (bei Anlaute und Lesezug: für das gewählte Erkennungsbild, umschaltbar).

Die Seite **Lernstand einlesen** (`lernstand.html`) liest die Codes ein und macht daraus druckbare Blätter
(ganze A4-Seite oder halbe Seite zum Einkleben ins Lernheft). Mehrere Codes nacheinander scannen, dann alle zusammen drucken.
Zugang: im Lehrerzimmer der Knopf **«Lernstand einlesen»** (geht auch ohne Anmeldung, Knopf auf der Anmeldeseite).

- Der Code enthält keinen Namen. Auf dem Blatt ist ein leeres Feld für den Namen von Hand.
- Die Seite speichert nichts. Die Kamera wird nur auf dem Gerät ausgewertet, nichts geht ins Internet.
  Sie ist bewusst getrennt vom Lehrerzimmer: Ihre Sicherheitsregel verbietet jede Verbindung, auch zum Lehrerzimmer-Server.
- Die Kamera funktioniert nur über `https` (GitHub Pages). Ohne Kamera: «Foto des Codes wählen».
- Tierbibliothek hat keinen Lernstand und darum keinen Code.

**Neue App anschliessen:** den Block zwischen `<!-- LERNSTAND-QR: Anfang -->` und `<!-- LERNSTAND-QR: Ende -->`
aus einer bestehenden App in den `<head>` der neuen App kopieren. Dann in der App
`LernstandQR.init({ app:'kennung', title:'Name', build(){ return { s:'Untertitel', b:[ …Blöcke… ] }; } })` aufrufen
und einen Knopf mit `LernstandQR.open()` auf die Startseite setzen. Mögliche Blöcke: `kpi`, `h`, `p`, `list`, `chips`,
`tab`, `grid`, `tiles`, `bars`, `spark`, `legend`, `cols` (Beispiele in den bestehenden Apps).
Die Seite `lernstand.html` muss dafür nicht geändert werden.

## Lehrerzimmer und Klassen-Boards

- `lehrerzimmer.html`: Plattform für Lehrpersonen (Zugang weiterhin über das Zahnrad auf dem Pausenplatz).
  App-Katalog mit Filtern (Klasse, Fachbereich, Dauer, LP21), Favoriten, Klassen-Boards als Wochenplan,
  Fokus-Modus, QR-Code und Link pro Board, Duplizieren, gemeinsames Bearbeiten, Rückmeldungen,
  Verwaltung (Einladungen, Lehrpersonen, Katalog, Meldungen).
- `klasse.html#CODE`: das Board der Klasse für die Kinder. Kein Login. Das Gerät merkt sich nur den Board-Code.
  Die Seite fragt alle 20 Sekunden nach, ob sich das Board geändert hat (z. B. Fokus-Modus).
- Server: Supabase-Projekt «Lehrerzimmer», Region Zürich (eu-central-2). Gespeichert werden nur
  Pseudonyme der Lehrpersonen, Boards und der App-Katalog. Keine Daten von Kindern.
- Konten: nur mit Einladungscode vom Admin. Keine E-Mail-Adresse; intern `pseudonym@lehrerzimmer.invalid`.
  Passwort vergessen: Admin setzt in der Verwaltung ein Einmal-Passwort.
- Neue App in den Katalog: in der Verwaltung → App-Katalog eintragen (eigene App: Pfad `apps/…html`).
  Der Pausenplatz selbst liest weiterhin `apps.js`.
- `.github/workflows/lehrerzimmer-wach-halten.yml` fragt einmal pro Tag den Katalog ab, damit Supabase
  das Gratis-Projekt nicht pausiert.

## Datenschutz

Die Startseite und alle Apps bauen keine Verbindungen ins Internet auf. Die Schriften sind direkt
in den HTML-Dateien eingebettet (alle unter SIL Open Font License), und jede Seite hat eine
Sicherheitsregel (`Content-Security-Policy`), die Anfragen nach aussen sperrt.

Ausnahme: In der Tierbibliothek öffnet der Knopf «Folge anschauen» die ARD Mediathek in einem neuen Tab,
aber erst, wenn ein Kind darauf tippt. Die Vorlesefunktion nutzt die Stimmen des Geräts.

Anlaute: Die App speichert keine Namen. Die Kinder wählen ein Bild als Erkennungszeichen, die
Zuordnung zu den Namen macht die Lehrperson auf Papier. Laute-Check und Übungsergebnisse bleiben
im Browser des jeweiligen iPads. Der PDF-Bericht wird auf dem Gerät erzeugt und heruntergeladen.

Blitzlicht: Die App speichert keine Namen und nur die Übung des Kindes, das gerade am Gerät ist.
Mit «Nächstes Kind» (Lehrpersonen-Bereich mit PIN) wird sie gelöscht. Vorgelesen wird nur mit einer
Premium-Stimme, die lokal auf dem Gerät läuft.

Lesezug: Die App speichert keine Namen. Die Kinder wählen ein Erkennungsbild (gleiche Nummern wie in der
Anlaute-App). Ergebnisse und Regler-Einstellungen bleiben im Browser des jeweiligen Geräts. Die Laute kommen aus
den eigenen Aufnahmen, Anleitungen und Wörter liest die normale Stimme des Geräts vor (keine Premium-Stimme).

Beim Einbauen einer neuen App darauf achten, dass sie keine Schriften oder Skripte von fremden
Adressen lädt (z.B. `fonts.googleapis.com`).
