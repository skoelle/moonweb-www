# AGENTS.md

## Globale Richtlinien

### Python / pip
- Niemals `pip install` direkt ausführen
- Immer ein virtuelles Umfeld (`python3 -m venv .venv`) anlegen und darin arbeiten
- `.venv` im Projektverzeichnis erstellen, bei Tests/Debugging nutzen

### Englisches Schreibstil
- `moonweb.org` immer klein schreiben (auch am Satzanfang)
- Kein "The" vor `moonweb.org` am Satzanfang setzen

### Lizenz
- Creative Commons Namensnennung - Nicht kommerziell - Weitergabe unter gleichen Bedingungen 4.0 International (CC BY-NC-SA 4.0)
- Copyright: Stefan Koelle — stefankoelle.de

## Build & Test

```bash
npm run build    # Build nach _site/
npm run dev      # Dev-Server auf http://localhost:8080
```

Mobile-Layout testen: Browser DevTools → Responsive Mode → 375px Breite.

## Mobile Layout (Responsive)

### Breakpoints
- `768px` — Haupt-Mobile-Layout
- `480px` — Kleinbildschirm-Zusätze

### Geänderte Dateien
- `src/_includes/layout.njk` — Mobile-Header (`div.mobile-header`) mit Logo, pageImage, Nav
- `src/_includes/nav.njk` — `details/summary`-Toggle
- `src/assets/css/moonweb.css` — Media Queries (Zeile ~90+)
- `src/css/nav-replacement.njk` — Background-Images im Mobile deaktivieren

### Mobile-Layout-Struktur
```
Logo (logomobile.gif, zentriert, margin 20px oben/links/rechts)
pageImage (108x120px, object-fit: cover, 1px Border) │ Navigation (Textlinks)
Content (volle Breite)
Quicknav (nur "beginning", Textlinks über Footer)
Footer
```

### Wichtige CSS-Klassen
- `.mobile-header` — Enthält Logo + nav-row
- `.mobile-logo` — logomobile.gif, `width: calc(100% - 40px)`, max 400px
- `.mobile-nav-row` — Flex-Row für pageImage + Nav, padding 20px
- `.mobile-pageimage` — 108x120px, `object-fit: cover`, 1px Border
- `.mobile-footer-quicknav` — Quicknav über Footer (nur Mobile sichtbar)

### Desktop-Layout unverändert
Alle Mobile-Änderungen sind in `@media (max-width: 768px)` gekapselt. Desktop (750px) wird nicht beeinflusst.

### Wichtig
Bei CSS-Änderungen am Mobile-Layout (Breakpoints, Klassen, Struktur) muss auch die AGENTS.md aktualisiert werden, damit die Dokumentation aktuell bleibt.
