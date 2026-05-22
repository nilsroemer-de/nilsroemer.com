# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Projektkontext

Persönliche Website von Dr. Nils Roemer unter `nilsroemer.com`. Die Seite dient als zentrale Anlaufstelle für seine Lehrtätigkeit mit modularem Lehrbereich (Kurse, Workshops). Für detaillierten Kontext → `kontext.md`.

## Wichtige Befehle

```bash
# Website lokal rendern und Preview starten
quarto preview

# Website bauen (Output in _site/)
quarto render

# Auf GitHub Pages deployen
quarto publish gh-pages
```

Nach dem Deployment ist die Seite unter `https://nilsroemer.com` erreichbar (Custom Domain via Strato → GitHub Pages).

## Projektstruktur

```
_quarto.yml       # Globale Konfiguration (Navigation, Theme, CSS)
index.qmd         # Startseite
about.qmd         # About-Seite (noch Platzhalter)
styles.css        # Custom CSS
_site/            # Generierter Output — nie manuell bearbeiten
kontext.md        # Projekthintergrund und Nächste Schritte
```

## Architektur

- **Quarto Website** (`type: website` in `_quarto.yml`): Jede `.qmd`-Datei wird zu einer HTML-Seite gerendert.
- **Navigation** wird zentral in `_quarto.yml` unter `website.navbar` konfiguriert — neue Seiten dort eintragen.
- **Theme:** Cosmo + Brand (`brand`-Theme erlaubt Custom Styling via `_brand.yml`, falls später hinzugefügt).
- **Deployment:** `quarto publish gh-pages` schreibt den gebauten `_site/`-Ordner in den `gh-pages`-Branch des GitHub-Repos. Der `main`-Branch enthält nur die Quelldateien.

## Neue Seiten anlegen

1. `.qmd`-Datei erstellen (z.B. `lehre/index.qmd` für den Lehrbereich)
2. In `_quarto.yml` unter `website.navbar` verlinken
3. `quarto preview` zum Testen, dann committen und `quarto publish gh-pages`
