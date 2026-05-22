# Projektkontext

## Projekt
Persönliche Website von Dr. Nils Roemer unter nilsroemer.com. Die Seite dient als zentrale Anlaufstelle für seine Lehrtätigkeit. Von der Startseite aus gelangt man zu einem Lehrbereich, der modular wächst: Kurse, Workshops und andere Lehrveranstaltungen werden nach und nach ergänzt, jeweils mit eigenen Unterlagen, Materialien und Inhalten.

Der erste Kurs ist noch nicht final festgelegt. Die technische Struktur wird so aufgebaut, dass Kurse einfach ergänzt werden können.

## Struktur (geplant)
- Startseite: Kurzvorstellung von Nils Roemer
- Lehre: Übersichtsseite mit allen Kursen und Workshops
  - Kurse und Workshops folgen modular

## Live-URL
https://nilsroemer.com

## GitHub Repository
https://github.com/Nilsthehustlertoast/my-test-course

## Lokaler Pfad Mac
/Users/nils/Projekte/my-test-course

## Tech-Stack
- Quarto 1.9.37 für die Website
- GitHub Pages für Hosting
- Custom Domain nilsroemer.com via Strato (A-Record auf GitHub Pages IP)
- Claude Code als Editor und KI-Assistent
- Git für Versionskontrolle

## Workflow
1. Änderungen in Claude Code vornehmen
2. `git add .`
3. `git commit -m "Beschreibung"`
4. `git push`
5. `quarto publish gh-pages`

## Aktueller Stand
- Startseite (index.qmd) vorhanden aber noch auf einen alten Kurs ausgerichtet, muss zur persönlichen Startseite umgebaut werden
- Domain nilsroemer.com eingerichtet und mit GitHub Pages verbunden
- Lehrbereich und Kursseiten fehlen noch

## Nächste Schritte
- Startseite zu persönlicher Vorstellungsseite umbauen
- Lehrbereich anlegen mit Übersichtsseite
- Ersten Kurs als Unterseite einbinden wenn Kursinhalt feststeht