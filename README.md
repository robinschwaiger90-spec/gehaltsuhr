# Gehaltsuhr

Sieh live zu, wie dein Gehalt tickt – als Sekunden-genaue "Uhr", die auf Basis von Monatsgehalt und Wochenstunden hochzählt. Zwei installierbare PWAs in diesem Repo:

- **[gehaltsuhr.html](gehaltsuhr.html)** – Handy-/Desktop-Version mit allen Details (Monat, Gesamtsumme seit Erster Arbeitstag, Vergleichswerte wie "wie lange arbeite ich für einen Kaffee")
- **[watch/](watch/index.html)** – abgespeckte Version fürs Handgelenk (Wear OS), große tickende Zahl, Einstellungen per Long-Press

Beide sind waschechte **Progressive Web Apps**: eigenes Manifest, Icons und Service Worker fürs Offline-Caching. Kein Server, kein Build-Schritt – reines HTML/CSS/JS.

## Lokal ausprobieren

Service Worker brauchen HTTPS oder `localhost`, `file://` reicht nicht. Lokal testen mit einem simplen Webserver:

```bash
python -m http.server 8791
```

Dann `http://localhost:8791/gehaltsuhr.html` bzw. `http://localhost:8791/watch/index.html` öffnen.

## Hosten (GitHub Pages)

1. Dieses Repo auf GitHub pushen
2. Repo-Einstellungen → **Pages** → Branch `main` (Root) aktivieren
3. App ist erreichbar unter `https://<username>.github.io/<repo>/gehaltsuhr.html`

## Auf dem Handy installieren

Seite im Browser öffnen → **„Zum Startbildschirm hinzufügen"**. Läuft danach wie eine native App (eigenes Icon, Vollbild, offline).

## Auf der Galaxy Watch installieren

Voraussetzung: Wear OS (Galaxy Watch4 oder neuer). `watch/index.html` im Watch-Browser öffnen → **„Zum Startbildschirm hinzufügen"**. Gehalt/Stunden einmal separat einrichten (Long-Press auf die Zahl) – Handy und Watch teilen sich keinen Speicher.

## Im Play Store veröffentlichen

1. App über GitHub Pages hosten (siehe oben) – Play Store braucht eine echte HTTPS-Domain
2. Auf [pwabuilder.com](https://www.pwabuilder.com) die gehostete URL eingeben → erzeugt ein signiertes Android App Bundle (Trusted Web Activity) inkl. `assetlinks.json`
3. `assetlinks.json` wie von PWABuilder angegeben unter `.well-known/assetlinks.json` im Repo ablegen, damit Play Store die Domain verifiziert
4. Account bei [Play Console](https://play.google.com/console) anlegen (einmalig 25 $), App anlegen, `.aab` hochladen, Store-Eintrag ausfüllen

## Daten

Alle Eingaben (Gehalt, Stunden, Arbeitsbeginn, Modus) landen nur lokal im `localStorage` des jeweiligen Geräts – es gibt keinen Server, keine Analyse, keinen Datenabfluss.
