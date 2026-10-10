# CLAUDE.md

Anleitung für Claude Code (claude.ai/code) beim Arbeiten in diesem Repository.

## Projektkontext

Persönliche Website von Dr. Nils Roemer unter `https://nilsroemer.com`. Sie stellt ihn als Unternehmer, Forscher und Lehrenden vor und bündelt seine Lehrtätigkeit (Übersicht der Kurse, Verweise auf Kurs-Websites). Die Seiteninhalte sind auf Englisch, die Kommunikation im Repo (Commits, diese Datei) auf Deutsch.

Der Name wird immer **„Roemer"** geschrieben, nie „Römer" – auch in Alt-Texten, Metadaten und Dateinamen.

## Infrastruktur

- **Hosting:** GitHub Pages aus dem Branch `gh-pages` des Repos `github.com/nilsroemer-de/nilsroemer.com` (Remote `origin`, SSH).
- **Branches:** `main` enthält ausschließlich die Quelldateien. `gh-pages` enthält nur den gebauten Output und wird allein von `quarto publish gh-pages` geschrieben – nie manuell.
- **Domain:** `nilsroemer.com` ist bei Strato registriert. Strato dient **nur als DNS** (A-Records auf die GitHub-Pages-IPs); dort wird nichts gehostet. DNS-Einstellungen nie anfassen.
- **CNAME:** Die Datei `CNAME` (Inhalt: `nilsroemer.com`) liegt im Repo-Root und ist in `_quarto.yml` unter `project.resources` eingetragen. Dadurch landet sie bei jedem Build in `_site/` und auf `gh-pages`, sonst verliert GitHub Pages die Custom Domain.
- **Keine CI/CD:** Es gibt keine GitHub Actions und keinen automatischen Deploy. Veröffentlicht wird ausschließlich manuell (siehe Workflow).
- **Toolchain:** Quarto 1.9.37, Git, Claude Code. Keine Node-/Python-Abhängigkeiten.

## Wichtige Befehle

```bash
quarto preview              # lokal rendern mit Live-Reload
quarto render               # Build nach _site/ (gitignored)
quarto publish gh-pages     # Deploy auf GitHub Pages → nilsroemer.com (nur auf Anweisung!)
```

## Workflow

**Veröffentlichen**

- `quarto publish gh-pages` wird **nur auf ausdrückliche Anweisung von Nils** ausgeführt. Ein Push auf `main` veröffentlicht nichts; erst `publish` ändert die Live-Seite.
- Vor dem Publish lokal mit `quarto render` prüfen, dass der Build fehlerfrei durchläuft.

**Kleine Änderungen** (Texte, Styling, einzelne Seiten)

- Direkt auf `main` arbeiten, committen und pushen (Commit-Messages auf Deutsch, wie in der Historie).

**Größere Umbauten** (neue Bereiche, Struktur-/Designänderungen, mehrere Seiten gleichzeitig)

- Mit den Superpowers-Skills arbeiten: Brainstorming → Plan → Umsetzung auf einem eigenen Branch in einem Git-Worktree (`superpowers:using-git-worktrees`).
- Am Ende das Ergebnis zeigen. **Erst nach Freigabe von Nils** in `main` mergen, dann den Branch und den Worktree aufräumen (`superpowers:finishing-a-development-branch`).
- Auch danach gilt: kein Publish ohne Anweisung.

## Projektstruktur

```
_quarto.yml        # Projektkonfiguration: Navbar, Footer, Theme, Resources (CNAME, fonts/)
_brand.yml         # Quarto-Brand: Farbpalette und Schriftfamilien (Planningio-Ableitung)
custom.scss        # @font-face (self-hosted), Design-Tokens als CSS-Variablen, Seitenkopf (h1/h2-Abstände), Eintrags-Layout, Navbar/Footer/Links
styles.css         # Nur Layout der Startseite (Foto + Text, Social-Links, Umbruch < 992 px)
index.qmd          # Startseite "About": Foto, Name als `#`-Überschrift, Kurzvorstellung, LinkedIn/E-Mail
cv.qmd             # Curriculum Vitae; Inhalt in `::: {.entries}` gewrappt (Eintrags-Layout, siehe Konventionen)
lectures.qmd       # Lehre: Kursübersicht im Eintrags-Layout (`::: {.entries}`), Links auf externe Kurs-Websites
imprint.qmd        # Impressum (Rechtstext)
privacy.qmd        # Datenschutzerklärung (Rechtstext)
CNAME              # Custom Domain für GitHub Pages
fonts/             # woff2-Dateien: Poppins, Inter, Space Mono (latin + latin-ext)
nils-roemer.jpg    # Porträtfoto der Startseite, 2100 × 1400 px (Querformat, per CSS als 4:5 beschnitten), ohne EXIF (© Xenia Bluhm)
DESIGN-TOKENS.md   # Referenz: Planningio-Design-System; vom Render ausgeschlossen
README.md          # Kurzbeschreibung des Repos
_site/             # Build-Output, gitignored, nie manuell bearbeiten
```

**Navigation:** Navbar (About · CV · Lectures) und Footer (Imprint · Privacy) werden zentral in `_quarto.yml` konfiguriert. Neue Seiten dort eintragen.

**Theme:** Cosmo + Brand + `custom.scss`, dazu `styles.css`. Das Design ist eine reduzierte Ableitung des Planningio-Brands (Navy/Blau, Poppins für Überschriften, Inter für Fließtext, Space Mono für Meta-Angaben). Nicht übernommen: Grapefruit-CTA-Farbe, Pill-Buttons, Drei-Balken-Motiv, Grain. Details in `DESIGN-TOKENS.md`.

## Konventionen

- **`pagetitle` statt `title`:** Im YAML-Header jeder Seite `pagetitle:` verwenden (setzt nur das `<title>`-Tag). Die sichtbare Überschrift steht als `# …` bzw. `## …` im Body. Grund: `custom.scss` blendet den Quarto-Title-Block aus; mit `title:` entstünde eine doppelte Überschrift im DOM.
- **Keine Requests an Dritte:** Alle Fonts sind self-hosted (`fonts/`, `@font-face` in `custom.scss`; der Google-Fonts-Import des Cosmo-Themes ist über `$web-font-path: false` abgeschaltet). Keine Analytics, keine Cookies, keine eingebetteten Fremdinhalte (Videos, Karten, CDN-Skripte). Die Datenschutzerklärung sichert genau das zu – jede neue Abhängigkeit muss dagegen geprüft werden.
- **Rechtstexte (`imprint.qmd`, `privacy.qmd`):**
  - Keine sichtbaren Datumsangaben („Stand: …", „Last updated …") einfügen.
  - Änderungen an Rechtstexten vor dem Einarbeiten als Vorschlag zeigen und von Nils freigeben lassen.
- **Inhaltsverzeichnis:** Global ist `toc: true`; Seiten ohne TOC setzen `toc: false` im Header (aktuell CV und Lectures).
- **Keine Gedankenstriche als Satzzeichen im sichtbaren Text.** Sätze stattdessen umformulieren (Komma, Punkt, Klammer). Bereichsangaben wie `2018–2022` und Seitenzahlen wie `271–286` bleiben.
- **Links im Inhalt:** Textfarbe, keine Unterstreichung, bei Hover Primärfarbe mit Unterstreichung. Global in `custom.scss` definiert, keine seitenspezifischen Abweichungen.
- **Seitenkopf:** Auf allen Seiten gleich, global in `custom.scss` definiert (Block „Page header"). Jede Seite beginnt mit genau einer `#`-Überschrift (auf der Startseite der Name), ohne Linie darunter, optional direkt gefolgt von einem Einleitungsabsatz. Die Abstände sind zentral festgelegt: oberhalb der h1 als `padding-top` auf `main` (`--space-6`), h1 → Inhalt als `margin-bottom` der h1 (`--space-5`), vor jedem Abschnittslabel als `margin-top` der h2 (`--space-7`). Keine seitenspezifischen Abweichungen in `.entries`, `styles.css` oder einzelnen Seiten; die Startseite übernimmt dieselben Maße, nur das Foto-Text-Layout ist dort zusätzlich.
- **Eintrags-Layout (`.entries`):** Gemeinsamer Stil für alle Inhaltsseiten mit der Struktur Abschnitt → Eintrag → Meta → Text (aktuell CV und Lectures). Seiteninhalt in `::: {.entries}` wrappen. Abschnitte als `##` (werden zu kleinen Uppercase-Labels), Rolle/Abschluss/Kurs als `###`, darunter Organisation und Zeitraum als eigene Zeile `[…]{.entry-meta}` (Space Mono, gedämpft), darunter Text oder Unterpunkte. Publikationen und Preise als einzelne Absätze ohne Aufzählungspunkte. Die Klassen sind bewusst nicht CV-spezifisch benannt; neue Seiten mit dieser Struktur nutzen dieselben Klassen statt eigener Styles.
- **Bilder:** Fotos vor dem Einchecken für Web komprimieren und EXIF-Metadaten entfernen; Auflösung so wählen, dass sie für Retina reicht (Porträt: 1400 px Höhe). Das Porträt wird per CSS (`object-fit: cover`, 4:5) beschnitten, ist gegen Rechtsklick/Drag geschützt; Bildnachweis unter dem Foto belassen.
- **Build-Artefakte** (`_site/`, `.quarto/`, `.DS_Store`) niemals committen.

## Stand und offene Punkte

**Stand**

- Live unter nilsroemer.com: Startseite/About, CV, Lectures, Imprint, Privacy. Letzter Publish am 10. Oktober 2026 (Stand `main` 739cc5b: „inspired by the book" in CV und Lectures).
- Design-Pass auf Planningio-Brand abgeschlossen, Fonts vollständig self-hosted, Rechtstexte vorhanden.
- Die Lehre-Seite verweist für den ersten Kurs („Programming: Everyday Decision-Making Algorithms", Kühne Logistics University) auf die externe Kurs-Website `courses.nilsroemer.com`. Kursinhalte liegen also nicht in diesem Repo.

**Offene Punkte**

- Ursprünglich geplanter modularer Lehrbereich (Übersicht + Kurs-Unterseiten innerhalb dieser Website): aktuell durch externe Kurs-Websites gelöst. Entscheiden, ob weitere Kurse hier oder extern leben.
- Optional: Favicon, Open-Graph-Metadaten, 404-Seite.
