# chromosphere-it.github.io

Zentrale Website von Chromosphere IT: Übersicht der Apps, Support-Seiten, Datenschutzerklärungen und Impressum. Live unter https://chromosphere-it.github.io/ (GitHub Pages, Branch `main`, Wurzelverzeichnis).

## Aufbau

| Pfad | Inhalt |
|---|---|
| `index.html` | Startseite: Logo, App-Karten, Kontakt, Hinweis zur Website selbst |
| `impressum.html` | Impressum nach § 5 DDG |
| `<app>/index.html` | Support-Seite der App |
| `<app>/privacy.html` | Datenschutzerklärung der App, nennt den Verantwortlichen |
| `style.css` | Gemeinsames Stylesheet im Look des Hugo-Themes [Terminal](https://github.com/panr/hugo-theme-terminal) (eigene Umsetzung, kein Theme-Code): dunkel, Fira Code, eckige Rahmen, gepunktete Titellinien, zentrierte Spalte (max. 864 px) mit feiner Akzentlinie links und rechts. Akzentfarbe pro App über die Body-Klasse (`jera`, `bcw`, `rista`, `crankoid`) |
| `fonts/` | Fira Code als woff2 (Latin, Latin Extended), selbst gehostet, Lizenz `fonts/OFL.txt` |
| `logo.png` | Logo (180×180), gleichzeitig Favicon und `apple-touch-icon` |
| `.nojekyll` | Schaltet Jekyll ab, die Seiten werden unverändert ausgeliefert |

Apps: `jera/`, `binaryclockwatch/`, `rista/`, `crankoid/` (Playdate, Download auf itch.io, Bestenliste auf crankoid.de).

## Regeln

- Jede Seite ist zweisprachig: Deutsch zuerst, danach Englisch in `<div lang="en">`.
- Einzige Kontaktadresse ist `ckdevel@me.com`.
- Keine externen Ressourcen (Fonts, CDNs, Skripte, Tracking). Außer den App-Store-Links wird nichts von außen geladen.
- Kein Gedankenstrich („—“) im Text.
- Jede Seite verlinkt im Footer das Impressum und hat die Favicon-Links im `<head>`.

## Neue App hinzufügen

1. `jera/` kopieren und in `<app>/` umbenennen, Texte, `<title>`, App-Store-Link und `aria-current` im Menü anpassen.
2. In `style.css` eine Akzentfarbe `body.<klasse>` ergänzen.
3. In `index.html` einen `<article class="post">`-Block ergänzen und in **allen** Seiten den Menüpunkt in `<nav class="menu">` nachtragen (Links sind wurzelrelativ, z.B. `/jera/`).
4. In App Store Connect die Support-URL `https://chromosphere-it.github.io/<app>/` und die Datenschutz-URL `https://chromosphere-it.github.io/<app>/privacy.html` eintragen, außerdem in `fastlane/metadata/*/support_url.txt` und `privacy_url.txt`.
5. Lokal prüfen (`python3 -m http.server`) und in Safari ansehen, dann pushen. Pages baut in weniger als einer Minute.

## Alte Adressen

Diese Repos sind nur noch Weiterleitungen. Nicht umbenennen, nicht löschen, Pages nicht abschalten, weil live Store-Versionen darauf verweisen:

| Alte URL | Ziel |
|---|---|
| `ckoys.github.io/jera-legal/#support` | `/jera/` |
| `ckoys.github.io/jera-legal/#datenschutz` | `/jera/privacy.html` |
| `ckoys.github.io/jera-legal/#privacy` | `/jera/privacy.html#privacy` |
| `ckoys.github.io/BinaryClockWatch-Support/` (+ `privacy.html`) | `/binaryclockwatch/` (+ `privacy.html`) |
| `chromosphere-it.github.io/Rista-Support/` (+ `privacy.html`) | `/rista/` (+ `privacy.html`) |

Die Weiterleitung passiert per JavaScript (`location.replace`, wertet bei Jera den Hash aus), mit `<noscript>`-Meta-Refresh und sichtbarem Link als Rückfallebene. Jera 1.0.2 und BinaryClockWatch 1.0.1 zeigen im Store noch auf die alten URLs, weil App Store Connect die URLs einer live Version sperrt (409). Die nächste Version bekommt die Hub-URLs.
