# 🌙 moonweb.org

Statische Website von [moonweb.org](https://www.moonweb.org), erstellt mit [Eleventy](https://www.11ty.dev/) als Static-Site-Generator.

## 🛠️ Technologie

- ⚡ **Eleventy 2.x** — Static-Site-Generator (Build-Time)
- 📝 **Nunjucks** — Template-Sprache für Layouts und Includes
- 📄 **Markdown** — Seiteninhalte
- 🎨 **HTML-Tabellen-Layout** — dreispaltiges Layout (1:1 wie das Original)

## 🚀 Starten

```bash
npm install
npm run dev      # 🔥 Dev-Server mit Live-Reload auf http://localhost:8080
npm run build    # 📦 Produktions-Build nach _site/
npm run clean    # 🧹 Build-Verzeichnis leeren
```

## 📁 Projektstruktur

```
moonweb-www/
├── .eleventy.js                 # ⚙️  Eleventy-Konfiguration
├── package.json
├── src/
│   ├── _includes/
│   │   ├── layout.njk           # 🏗️  Master-Layout (3-Spalten-Tabellen)
│   │   ├── nav.njk              # 🧭 Rechte Seiten-Navigation
│   │   ├── quicknav.njk         # ⚡ Linke Quicknav-Box
│   │   └── redirect.njk         # ↪️  Meta-Refresh-Weiterleitung
│   ├── _data/
│   │   ├── nav.json             # 📋 Menüstruktur (8 Sektionen, 4 Gruppen)
│   │   └── site.json            # 🌐 Globale Daten (Domain, Kontakt-E-Mail)
│   ├── css/
│   │   └── nav-replacement.njk  # 🎨 Generiert nav-replacement.css
│   ├── assets/
│   │   ├── css/moonweb.css      # 🎨 Haupt-Stylesheet
│   │   ├── images/              # 🖼️  Layout-Bilder, Favicon (10 Dateien)
│   │   ├── menu/                # 🍔 Nav-Sprite-GIFs (24 Dateien: 8×3 Zustände)
│   │   ├── pageImage/           # 📸 Sektions-Header-Bilder (10 Dateien)
│   │   ├── content/             # 🖼️  Inline-Bilder (2 Dateien)
│   │   └── archive/             # 📦 Archiv-Banner und Splash-Screens
│   ├── beginning/               # 🌟 Sektion "beginning" (Startseite + Unterpunkte)
│   ├── projects/                # 🚀 Sektion "projects"
│   ├── products/                # 📦 Sektion "products"
│   ├── acoustics/               # 🎵 Sektion "acoustics"
│   ├── location/                # 📍 Sektion "location"
│   ├── background/              # 🎭 Sektion "background"
│   ├── partners/                🤝 Sektion "partners"
│   ├── contact/                 # 📞 Sektion "contact"
│   ├── network/                 # 🌐 Sektion "network" (kein Nav-Eintrag)
│   ├── stefan/                  # 👤 Sektion "stefan" (kein Nav-Eintrag)
│   ├── index.md                 # 🏠 Startseite
│   ├── robots.njk               # 🤖 Generiert robots.txt
│   └── sitemap.xml.njk          # 🗺️  Generiert sitemap.xml
```

## 🧭 Navigation

Die Navigation besteht aus 8 Sektionen in 4 Gruppen:

| Gruppe | Sektionen |
|--------|-----------|
| 1 | 🌟 beginning |
| 2 | 🚀 projects, 📦 products, 🎵 acoustics |
| 3 | 📍 location, 🎭 background, 🤝 partners |
| 4 | 📞 contact |

Zusätzlich existieren die Sektionen `network` und `stefan` mit Inhalten, die jedoch nicht in der Hauptnavigation erscheinen.

## ⚙️ Technische Details

- **Layout:** 📐 Dreispaltige HTML-Tabelle (108px linke Sidebar | Inhaltsbereich | 150px rechte Sidebar)
- **Navigation:** 🎯 CSS-Hover-Effekte statt JavaScript (reine Bild-Tausch-Technik via `text-indent: -9999px`)
- **Shortcode:** 📦 `pseudonymBox` — rechtsbündige Box mit dunklem Hintergrund und Gold-Überschrift
- **Routing:** ↪️ Alte URL-Pfade werden via Meta-Refresh auf die neue Startseite weitergeleitet

## 📱 Mobile Layout (Responsive)

Das mobile Layout wird per CSS Media Query bei `max-width: 768px` aktiviert. Die Desktop-Version (750px) bleibt unverändert.

### Geänderte Dateien

| Datei | Änderung |
|-------|----------|
| `src/_includes/layout.njk` | Mobile-Header (`div.mobile-header`) mit Logo, pageImage und Navigation |
| `src/assets/css/moonweb.css` | Media Queries für Mobile (768px) und Kleinbildschirm (480px) |
| `src/_includes/nav.njk` | `details/summary`-Toggle für CSS-only Mobile-Menü |
| `src/css/nav-replacement.njk` | Mobile-Regel: Background-Images deaktivieren |

### Mobile-Layout-Struktur

```
┌─────────────────────────────┐
│  Logo (logomobile.gif)      │  ← zentriert, 20px Margin oben/links/rechts
│  1px schwarzer Border       │
├─────────────────────────────┤
│  pageImage │ Navigation     │  ← Flex-Row, pageImage links (108x120px, beschnitten)
│  1px Border│ Textlinks      │    mit 20px Padding, Navigation rechts daneben
├─────────────────────────────┤
│  Content (volle Breite)     │
├─────────────────────────────┤
│  Quicknav (falls vorhanden) │  ← nur in "beginning", Textlinks zentriert
├─────────────────────────────┤
│  Footer                     │
└─────────────────────────────┘
```

### Was passiert im Mobile-Modus

- **Layout:** Tabellen auf `display: block` umgeschaltet, volle Breite
- **Linke Sidebar:** Komplett ausgeblendet
- **Rechte Sidebar:** Komplett ausgeblendet (Nav + Logo im mobile-header)
- **Navigation:** Inline Textlinks rechts neben pageImage (kein Hamburger-Menü)
- **pageImage:** 108px breit, 120px hoch (mit `object-fit: cover`, oben abgeschnitten)
- **Logo:** `logomobile.gif`, skaliert auf `calc(100% - 40px)`, max 400px, zentriert
- **Hintergrund:** Komplett deaktiviert
- **Quicknav:** Textlinks über Footer (nur in "beginning"-Sektion)
- **Typografie:** Schriftgröße 14px (statt 9pt), h1 margin 0
- **Formulare:** `width: 100%`, `max-width: 100%`
- **Bilder:** `max-width: 100%`, `height: auto`

### Kleinbildschirm (480px)

Zusätzliche Anpassungen für sehr kleine Bildschirme:
- Schriftgröße 13px
- h1 Schriftgröße 16pt
- Reduziertes Padding im Content-Bereich

## 📜 Lizenz

Dieses Projekt steht unter der [Creative Commons Namensnennung - Nicht kommerziell - Weitergabe unter gleichen Bedingungen 4.0 International](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.de) (CC BY-NC-SA 4.0).

Copyright (c) Stefan Koelle — [stefankoelle.de](https://stefankoelle.de)
