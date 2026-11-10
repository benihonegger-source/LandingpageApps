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
