# Sammelbuch

Dein digitales Boulder-Jahressammelbuch: ein Tap nach der Halle, und dein Jahr füllt sich Zug für Zug. Kein Account, kein Server, kein Routen-Tagebuch-Zwang – nur deine Besuche, dein Ziel und ein bisschen Send.

## Was die App kann

- Stempelt einen Boulderhallen-Besuch für den heutigen Tag und zeigt Jahres-, Monats- und Streak-Statistiken.
- Erfasst für jeden Besuch eine Anstrengungsstufe und optionale Boulder-Grade.
- Schaltet Erfolge frei, zeigt ein tägliches Boulder-Horoskop und führt eine gemeinsame Wochen-Streak mit einem Buddy.
- Lässt vergangene Tage nachtragen und frühere Jahre anzeigen.
- Speichert alle Daten im `localStorage` des Browsers und kann sie als JSON-Backup exportieren bzw. wieder importieren.
- Installiert sich als Progressive Web App (PWA). App-Shell und Laufzeitbibliotheken werden beim ersten erfolgreichen Laden gecacht; Google Fonts werden bei Bedarf nachgeladen und zwischengespeichert.

## Starten

Es gibt keinen Build-Schritt und keine Paketabhängigkeiten. Die App besteht aus einer HTML-Datei, einem Manifest, einem Service Worker und SVG-Icons.

Öffne [`Sammelbuch.html`](Sammelbuch.html) über einen statischen Webserver, zum Beispiel:

```sh
python3 -m http.server 8000
```

Anschließend `http://localhost:8000/` im Browser öffnen. Die Startseite leitet auf `Sammelbuch.html` weiter.

Für PWA-Installation und den Service Worker muss die App über `http://localhost` oder HTTPS laufen; ein direktes Öffnen als Datei (`file://`) reicht dafür nicht aus.

## Benutzung

1. Beim ersten Start ein Jahresziel wählen.
2. Nach der Session auf **„Heute gebouldert“** tippen.
3. Über das Zahnrad lassen sich Akzentfarbe, Ziel, Animation und Buddy-Name ändern, Tage nachtragen sowie Backups sichern oder laden.
4. Die Tabs unten wechseln zwischen Sammeln, Erfolgen und Jahr.

Die Daten bleiben bewusst auf dem jeweiligen Gerät und Browserprofil. Ein Browserdaten-Reset entfernt sie; vor einem Geräte- oder Browserwechsel deshalb im Bereich **Daten** ein Backup herunterladen und danach wieder importieren.

## Projektstruktur

| Datei | Aufgabe |
| --- | --- |
| [`Sammelbuch.html`](Sammelbuch.html) | Gesamte React-Oberfläche und lokale Datenspeicherung |
| [`index.html`](index.html) | Einstieg mit Weiterleitung zur App |
| [`manifest.json`](manifest.json) | PWA-Metadaten und Icons |
| [`sw.js`](sw.js) | Service Worker und Cache-Strategien |

## Technische Hinweise

React, ReactDOM und Babel werden zur Laufzeit von `unpkg.com` geladen. Für den ersten vollständigen App-Start wird daher eine Netzwerkverbindung benötigt. Danach bedient der Service Worker die App-Shell und diese Skripte cache-first; andere Inhalte verwenden network-first mit Cache-Fallback.

Zum Entwickeln reicht ein moderner Browser. Änderungen an `sw.js` oder den geladenen App-Ressourcen sollten mit einer neuen `CACHE_NAME`-Version ausgerollt werden, damit vorhandene Installationen den aktualisierten Cache aktivieren.
