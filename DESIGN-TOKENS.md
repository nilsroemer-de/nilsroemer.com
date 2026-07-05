# Planningio — Design Tokens

Extrahiert aus dem Hugo-Projekt **`/Users/nils/Projekte/planning_website/website`**
(read-only analysiert, nichts verändert). Quellen der Wahrheit:

- `assets/css/tokens.css` — Farben, Typo-Foundations, Radii, Shadows, Spacing, Font-Familien/-Gewichte
- `assets/css/brand.css` — Marken-Motive & Primitive (Buttons, Cards, Drei-Balken-Marke, Grain, Sky-Fields)
- `assets/css/site.css` — Seitenlayout (Header/Footer, Links, Container, Responsive)
- `assets/css/fonts.css` — `@font-face`-Deklarationen (self-hosted woff2)
- `layouts/_default/baseof.html`, `partials/header.html`, `partials/footer.html` — Einbindung & Struktur
- `static/img/` — Logos

**Marken-Charakter** (aus den Kommentaren): *„Light, airy, confident."* Tiefes Navy + klares Blau als Basis, Grapefruit-Rot als sparsam eingesetzter Energie-Akzent, weiche runde Formen, blau getönte Schatten, dezenter Film-Grain.

**Fonts:** vollständig self-hosted (`/fonts/*.woff2`), **keine** Laufzeit-Requests an Google Fonts (im Quellcode verifiziert: 0 Treffer). CSS wird in Hugo gebündelt (`fonts.css → tokens.css → brand.css → site.css`), minifiziert und mit SHA-256 fingerprinted; `poppins-700.woff2` wird preloaded.

---

## 1. Farbpalette

### Brand Core
| Token | Hex | Verwendung |
|---|---|---|
| `--pio-ink` | `#1e2648` | Tiefstes Navy — Headlines, Logo-Wordmark, Text auf hell; Footer-Band-Hintergrund |
| `--pio-primary` | `#01579b` | Primärblau — Links, primäre Aktionen, Key-Accents |
| `--pio-primary-light` | `#85bae3` | Hellblau — sekundäre Flächen, 2. Logo-Balken |
| `--pio-primary-faint` | `#d2e7f8` | Zartblau — Tints, 3. Logo-Balken, Hover-Wash |
| `--pio-milk` | `#edf1f5` | „Milk" — App-Canvas, Section-Hintergründe |
| `--pio-white` | `#ffffff` | Reinweiß |

### Sky-Surface-Familie (Hero-/Illustrations-Hintergründe)
| Token | Hex | Verwendung |
|---|---|---|
| `--pio-sky-100` | `#f3f8fd` | Fast-weißes Blau, Page-Tint |
| `--pio-sky-200` | `#e7f1fb` | Weicher Hero-Wash |
| `--pio-sky-300` | `#cfe2f4` | Card-auf-Sky, Divider |
| `--pio-sky-500` | `#9cc6e8` | Mid-Sky (Illustrationsfläche), Wave-Grundfarbe |

### Beverage-Akzente (sparsam einsetzen)
| Token | Hex | Verwendung |
|---|---|---|
| `--pio-grapefruit` | `#e94450` | Primäre CTA / High-Energy-Momente |
| `--pio-rose` | `#f0867f` | Weicheres Pink — Badges, Gradient-Partner zu Grapefruit |

CTA-Buttons nutzen einen vertikalen Verlauf `--pio-rose → --pio-grapefruit` (`180deg`).

### Daten-/Chart-Palette (Gantt-Bars, Donut-Segmente, Status-Fills)
| Token | Hex | Bedeutung |
|---|---|---|
| `--pio-data-blue` | `#2e6da4` | scheduled / running |
| `--pio-data-sky` | `#7fb1da` | queued / light |
| `--pio-data-teal` | `#2ec4a6` | complete / optimal |
| `--pio-data-indigo` | `#2b2be0` | highlight / selected |
| `--pio-data-purple` | `#8b5cf6` | category / cleaning |
| `--pio-data-amber` | `#f5b83d` | attention / filling |

### Text
| Token | Hex | Verwendung |
|---|---|---|
| `--pio-fg-1` | `#1e2648` | Primärtext (= ink) |
| `--pio-fg-2` | `#4a5578` | Sekundärtext — gedämpftes Navy (Lead, Captions) |
| `--pio-fg-3` | `#8a93ad` | Tertiär / Captions / Placeholder |
| `--pio-fg-on-dark` | `#ffffff` | Text auf dunklem Grund |
| `--pio-fg-on-primary` | `#ffffff` | Text auf Primärblau |
| `--pio-link` | `#01579b` | Link-Farbe (= primary) |

### Borders & Lines
| Token | Hex | Verwendung |
|---|---|---|
| `--pio-border` | `#dde5ee` | Standard-Haarlinie |
| `--pio-border-strong` | `#c3d2e2` | Betont (z. B. Outline-Buttons, Lang-Toggle) |
| `--pio-border-faint` | `#eef3f8` | Sehr zart (getönte Cards) |

### Semantische Status
| Token | Hex |
|---|---|
| `--pio-success` | `#2ec4a6` |
| `--pio-info` | `#01579b` |
| `--pio-danger` | `#e94450` |

### Tonale Section-Bänder (site.css)
- `.band-sky` — Verlauf `white → sky-100 (26%) → sky-300`
- `.band-milk` — Fläche `--pio-milk`
- `.band-white` — Fläche weiß
- `.band-ink` — Fläche `--pio-ink`, Text weiß (Footer & „Reference"-Sektion)

---

## 2. Typografie

### Familien
| Rolle | Stack | Einsatz |
|---|---|---|
| Display / Heading | `"Poppins", system-ui, sans-serif` | Alle Headlines, UI-Titel, Buttons, Nav, Eyebrows |
| Body | `"Inter", "Source Sans 3", system-ui, -apple-system, sans-serif` | Fließtext, Lead, Captions |
| Mono | `"Space Mono", ui-monospace, Menlo, monospace` | Meta, Tags, Lang-Toggle, technische Labels |

> Hinweis aus tokens.css: Das eigentliche Logo ist in *Tw Cen MT* gesetzt (Paid Font); **Poppins** ist der frei verfügbare Marken-Ersatz für alle Headings.

### Font-Einbindung (self-hosted, `fonts.css`)
Alle als `woff2`, `font-display: swap`, Pfad `/fonts/…`:
- **Poppins**: 400, 500, 600, 700
- **Inter**: 400, 500, 600, 700
- **Space Mono**: 400, 700

Dateien liegen in `assets/fonts/` (`poppins-400.woff2` … `spacemono-700.woff2`). `poppins-700.woff2` wird via `<link rel="preload">` vorgeladen.

### Gewichte
| Token | Wert |
|---|---|
| `--pio-w-regular` | 400 |
| `--pio-w-medium` | 500 |
| `--pio-w-semibold` | 600 |
| `--pio-w-bold` | 700 |

### Type-Skala (semantische Klassen, tokens.css)
| Klasse | Familie | Gewicht | Größe | line-height | letter-spacing | Farbe |
|---|---|---|---|---|---|---|
| `.pio-display` | Poppins | 700 | `clamp(40px, 6vw, 72px)` | 1.02 | −0.02em | ink |
| `.pio-h1` | Poppins | 700 | 44px | 1.08 | −0.018em | ink |
| `.pio-h2` | Poppins | 500 | 32px | 1.15 | −0.012em | ink |
| `.pio-h3` | Poppins | 600 | 24px | 1.25 | −0.006em | ink |
| `.pio-h4` | Poppins | 600 | 19px | 1.3 | — | ink |
| `.pio-lead` | Inter | 400 | 20px | 1.55 | — | fg-2 |
| `.pio-body` | Inter | 400 | 16px | 1.6 | — | fg-1 |
| `.pio-small` | Inter | 400 | 14px | 1.5 | — | fg-2 |
| `.pio-caption` | Inter | 500 | 12px | 1.4 | — | fg-3 |
| `.pio-eyebrow` | Poppins | 700 | 13px | 1.2 | +0.14em, UPPERCASE | primary |
| `.pio-mono` | Space Mono | 400 | 13px | 1.5 | — | fg-2 |

Body-Grundwerte (site.css): `body { font-family: Inter; color: fg-1; background: white; -webkit-font-smoothing: antialiased; text-rendering: optimizeLegibility; }`

---

## 3. Gestaltungsmerkmale

### Spacing (4px-Basis)
`--pio-space-1..9` = 4, 8, 12, 16, 24, 32, 48, 64, 96 px.
Section-Padding: `.sec-pad` = `clamp(64px, 8vw, 104px)` vertikal; `.sec-pad-s` = `clamp(48px, 6vw, 80px)`.
Container: `.wrap` max 1080px · `.wrap-n` max 820px (textlastig) · `.wrap-w` max 1180px; Seitenpadding 40px (→ 22px < 600px).

### Border-Radius
| Token | Wert | Einsatz |
|---|---|---|
| `--pio-r-xs` | 6px | kleine Tags |
| `--pio-r-sm` | 10px | |
| `--pio-r-md` | 14px | Default-Card / Icon-Kachel |
| `--pio-r-lg` | 20px | große Cards / Panels |
| `--pio-r-xl` | 28px | Hero-Blöcke / Video-Card |
| `--pio-r-pill` | 999px | Pill-Buttons (Motiv „TERMIN BUCHEN"), Lang-Toggle, Badges |

### Schatten (weich, low-contrast, blau getönt — auf `rgba(30,38,72,…)`)
| Token | Wert |
|---|---|
| `--pio-shadow-xs` | `0 1px 2px rgba(30,38,72,.06)` |
| `--pio-shadow-sm` | `0 2px 8px rgba(30,38,72,.07)` |
| `--pio-shadow-md` | `0 8px 24px rgba(30,38,72,.09)` |
| `--pio-shadow-lg` | `0 20px 48px rgba(30,38,72,.12)` |
| `--pio-shadow-cta` | `0 10px 24px rgba(233,68,80,.30)` (Grapefruit-Glow, nur unter der primären CTA) |

### Buttons (`brand.css`)
Basis `.pio-btn`: Poppins **700**, 16px, Pill-Radius, Padding `16px 30px`, `gap 10px`, Transition auf transform/shadow/color; `:active` → `translateY(1px) scale(.99)`.
- `.pio-btn-cta` — Grapefruit-Verlauf (`rose→grapefruit`), weiß, UPPERCASE, `letter-spacing .04em`; Hover hebt an (`translateY(-1px)`) + tieferer Schatten. `.pio-btn-cta-glow` fügt den Grapefruit-Glow hinzu (nur Hero-CTA).
- `.pio-btn-primary` — Fläche `--pio-primary`, weiß; Hover `#014a85`.
- `.pio-btn-secondary` — weiß, Primärtext, `1.5px` Border `border-strong`; Hover Border→primary, BG→sky-100.
- `.pio-btn-ghost` — transparent, fg-2; Hover ink auf sky-100.
- Größen: `.pio-btn-sm` (`10px 18px`, 14px) · `.pio-btn-lg` (`20px 38px`, 18px).

### Link-Verhalten
- **Nav-Links** (`.nav-link`): Poppins medium, 15px, fg-2; Hover→ink; animierter Unterstrich als 3-Farben-Gradient (`ink→primary-light→primary-faint`), wächst von 0→100 % (`.nav-link::after`, `aria-current` = aktiv).
- **Prose-/Inline-Links** (`.pio-body a`, `.legal a`): ink-Text mit `1px` primary-Unterstrich; Hover→primary-Text. (Kein klassisches Blau-Underline, sondern ruhige Border-Bottom.)
- **Footer-Links**: `rgba(255,255,255,.7)`; Hover weiß.
- **Scroll-Link** (`.link-scroll`): Poppins semibold, primary, Icon animiert nach unten bei Hover.

### Cards
`.pio-card`: weiß, `1px` border, `r-lg`, `shadow-sm`, Padding `space-6 (32px)`. `.pio-card-hover` → `translateY(-4px)` + `shadow-md`. `.pio-card-tint`: BG sky-100, border-faint.
Wiederkehrendes Hover-Muster für Kacheln (`step-card`, `out-item`, `proc-step`, `twin-tile`, `mod-plug`): Lift `top:-4px` + `shadow-md` **und** 3px-Gradient-Akzentlinie oben (`ink→primary-light→primary-faint`), die von 0→100 % wächst.

### Navbar (`header.html` + site.css)
- Sticky (`top:0`, `z-index:50`), Höhe **72px**, `justify-content: space-between`.
- Hintergrund `rgba(255,255,255,.82)`; **Frosted Glass** nur ≥921px (`backdrop-filter: saturate(1.4) blur(12px)`).
- `.is-stuck` (gescrollt) blendet Bottom-Border (`--pio-border`) + `shadow-xs` ein.
- Links: Brand-Logo (Color-PNG, angezeigt 120×26). Mitte/rechts: Nav-Liste (gap 30px), Sprach-Umschalter (Pill), Mobile-Menü-Button.
- Sprach-Toggle: Pill mit `border-strong`, Buttons in Space Mono 12px; aktiver Zustand BG primary/weiß.
- < 920px: Desktop-Nav aus, Burger ein → Vollflächen-Drawer (`--pio-milk`-BG + Radial-Tint + Film-Grain), Nav-Links 28px zentriert.

### Footer (`footer.html` + site.css)
- Dunkles `.band-ink`-Band, Padding `40px 0`, `.footer-inner` als space-between-Flex (umbrechend).
- Legal-Links links (Imprint/Privacy, aus i18n), rechts `.footer-meta` in Space Mono 13px („Hamburg, DE · built by … · designed by … · video by …") mit unterstrichenen Partner-Links.
- HTML-Grundfläche (`html`) ist `--pio-ink`, damit Overscroll unter dem Footer zur Footer-Farbe passt.

### Signatur-Motive (`brand.css`)
- **Drei-Balken-Marke** (`.pio-bars`): drei vertikale Balken, gestuft `ink → primary-light → primary-faint`, **eckige** Kanten (wie das Logo). Wiederverwendet als Section-Marker, Bullets, Hover-Unterstrich-Gradient. Animierte Variante `.anim-bars` (Balance-„Atmen").
- **Film-Grain** (`.pio-grain` / `.pio-grain-soft`): inline SVG-Fractal-Noise via `::after`, `mix-blend-mode: soft-light`, Opazität .5 / .28.
- **Sky-Fields** (`.pio-sky-soft`, `.pio-sky-deep`): radiale Blau-Verläufe als Hero-/Illustrationsgrund.
- **Waves** (`.pio-waves`): mehrere geschichtete Sinus-Wellen (SVG-Tiles), horizontale Parallax-Drift (14s), respektiert `prefers-reduced-motion`.
- Durchgehend `prefers-reduced-motion`-Guards für alle Animationen; `.reveal` ist transform-only (Inhalt bleibt bei No-JS/Print sichtbar).

---

## 4. Logo & Bildsprache

Alle in `static/img/` (ausgeliefert unter `/img/…`):
| Datei | Maße (px) | Format | Variante / Einsatz |
|---|---|---|---|
| `planningio-logo-color.png` | 1400 × 274 | PNG (transparent) | Farb-Wordmark auf hellem Grund — Header/Brand |
| `planningio-logo-white.png` | 1400 × 274 | PNG (transparent) | Weiße Wordmark für dunkle Bänder (Footer/ink) |
| `planningio-mark.png` | 1252 × 1250 | PNG (~quadratisch) | Reine Bildmarke (Drei-Balken-Icon) |
| `favicon/planningio-app-icon.png` | — | PNG | Favicon / App-Icon (`<link rel="icon">`) |

- **Seitenverhältnis Wordmark:** ~5.1:1 (1400×274); im Header auf `height:26px` skaliert (≈120×26), im Footer `height:24px`.
- **Kein SVG-Logo** vorhanden — nur PNG. Die Drei-Balken-Idee existiert zusätzlich als reines CSS-Motiv (`.pio-bars`), das ohne Bilddatei skaliert.
- **Farbvarianten:** Color (für hell) + White (für dunkel). Icon separat als quadratische Mark.

### Ergänzende Bild-/UI-Sprache
- Illustrationen und Diagramme sind großteils **inline SVG** (Loop, Network-DAG, Modules — `partials/svg/*`), gefärbt über die Token-Variablen (`--pio-primary`, `--pio-grapefruit`, `--pio-data-*`).
- Icons: Inline-SVG-Sprite (`.ic`, `stroke: currentColor`, `stroke-width 1.9`, runde Caps).
- Hero-Video als abgerundete Card (`r-xl`) mit tiefem Schatten, Play-Button im Grapefruit-Verlauf.

---

## 5. Mapping-Hinweise für eine Quarto `_brand.yml`

> (Noch **nicht** angelegt — nur zur Vorbereitung des nächsten Schritts.)

Quarto-`_brand.yml` kennt v. a. `color.palette` + semantische Rollen und `typography` mit `fonts` (Quelle `file`/`google`) sowie `base`/`headings`/`monospace`. Vorschlag zur Ableitung:

**`color.palette`** (Named Colors 1:1 übernehmen): `ink #1e2648`, `primary-blue #01579b`, `primary-light #85bae3`, `primary-faint #d2e7f8`, `milk #edf1f5`, `sky-100..500`, `grapefruit #e94450`, `rose #f0867f`, Border-/fg-Töne.

**`color` (semantisch):**
- `foreground: ink (#1e2648)`
- `background: white (#ffffff)` — alternativ `milk` für getönte Flächen
- `primary: #01579b`
- `secondary: #4a5578` (fg-2)
- `success: #2ec4a6` · `info: #01579b` · `danger: #e94450` · `warning: #f5b83d`
- `link: #01579b`

**`typography`:**
- Fonts self-hosten (wie bei nilsroemer.com bereits gemacht): `Poppins` (400/500/600/700), `Inter` (400/500/600/700), optional `Space Mono` (400/700) — als `source: file` mit den woff2, **nicht** `google`, um DSGVO-konform zu bleiben.
- `base: Inter`, ~16px, line-height 1.6
- `headings: Poppins`, Gewicht 600–700, tighter line-height (1.08–1.25), negatives letter-spacing (~−0.01…−0.02em)
- `monospace: Space Mono`
- `link`: dezent — ink-Text mit primary-Unterstrich statt Vollblau (aus site.css übernehmen, ggf. via zusätzlichem SCSS-Layer, da `_brand.yml` das Underline-Detail nicht abbildet).

**Radii/Shadows/Spacing:** von `_brand.yml` nicht nativ abgedeckt → in einem begleitenden `custom.scss` als CSS-Variablen spiegeln (Pill-Buttons `999px`, Card `20px`, weiche blau-getönte Schatten).

**Achtung Namensraum:** In `params.toml` steht `company.name = "BeyondSimulations"` neben `legalName = "PLANNINGIO GmbH"` — für nilsroemer.com irrelevant, nur zur Kenntnis.
