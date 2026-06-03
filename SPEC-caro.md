# SPEC.md — Caro (Landing Page)

> Minimalistische Landing-Page in Schwarz-Weiß mit Vollbild-Hintergrundvideo.
> Stil-Vorbild: https://aimedcapital.vercel.app
> Entwicklung mit **Claude Code**, Versionierung **GitHub**, Hosting **Vercel**.

---

## 1. Ziel

Eine reduzierte, elegante Platzhalter-Seite für Caro. Großes
Hintergrundvideo, eine ruhige Typo-Headline, drei nummerierte Menüpunkte
(**01 · 02 · 03**). Alle Inhalte sind aktuell **„Under Construction"** —
die Seite signalisiert „kommt bald", wirkt aber fertig und hochwertig.

---

## 2. Tech-Stack

| Bereich      | Wahl                          | Begründung |
|--------------|-------------------------------|------------|
| Aufbau       | Statisches **HTML + CSS + minimal JS** | Maximal schlank, schnell, kein Build nötig |
| Hosting      | **Vercel**                    | Null-Config, automatische Deploys aus GitHub |
| Versionierung| **GitHub**                    | Manuelles Pushen durch Nutzer |
| Video        | Lokale `hero-bg.mp4` in `/public` (bzw. Root) | Wird vom Nutzer selbst hochgeladen |

Bewusst **kein** Framework, kein Tracker, keine Cookies.

---

## 3. Designsprache

- **Strikt Schwarz-Weiß.** Hintergrund schwarz (`#000`), Text weiß (`#fff`),
  Grautöne nur für Sekundärtext (`rgba(255,255,255,.55)`) und feine Linien
  (`rgba(255,255,255,.15)`).
- **Typografie:** eine klare serifenlose Schrift (z.B. `Inter` oder
  System-Sans). Große, leichte Headline; weite Buchstabenabstände (`letter-spacing`)
  für Labels und Nummern.
- **Hintergrundvideo** deckt den ganzen Viewport, leicht abgedunkelt
  (dunkles Overlay), entsättigt/`grayscale`, damit es schwarz-weiß bleibt.
- **Viel Negativraum**, klare Ausrichtung, keine Verspieltheit.

---

## 4. Aufbau der Seite (eine Ansicht, kein Scrollen nötig)

```
┌──────────────────────────────────────────┐
│  [Video Vollbild, grayscale + dark overlay]│
│                                            │
│  CARO                          (Logo/Wortmarke, oben links)
│                                            │
│         (Headline mittig/links)            │
│         Caro                               │
│         Under Construction.                │
│         kurzer Untertitel-Satz             │
│                                            │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐   │
│  │ 01       │ │ 02       │ │ 03       │   │
│  │ Titel    │ │ Titel    │ │ Titel    │   │
│  │ under    │ │ under    │ │ under    │   │
│  │ constr.  │ │ constr.  │ │ constr.  │   │
│  └──────────┘ └──────────┘ └──────────┘   │
│                                            │
│  Frankfurt · DE            Kontakt (Footer)│
└──────────────────────────────────────────┘
```

### Komponenten
1. **Hintergrundvideo** — `autoplay muted loop playsinline`, `object-fit: cover`,
   Filter `grayscale(100%)`, dunkles Overlay darüber für Lesbarkeit.
2. **Wortmarke** „Caro" oben links, klein, mit Letter-Spacing.
3. **Hero-Text** — großer Titel „Caro", darunter „Under Construction." und
   ein kurzer Satz (Platzhalter, vom Nutzer anpassbar).
4. **Drei Karten 01 / 02 / 03** — je große Nummer, ein Platzhalter-Titel und
   der Status „Under Construction". Karten sind dezent umrandet
   (1px weiße Linie, leichtes Hover: minimal aufhellen). Aktuell **nicht
   verlinkt** (alles in Bau) — Klick optional deaktiviert oder führt auf `#`.
5. **Footer** — Ort („Frankfurt · DE" o.ä.) und ein Kontakt-Platzhalter.

---

## 5. Inhalte (Platzhalter — vom Nutzer zu füllen)

- Headline: **Caro**
- Status: **Under Construction**
- Untertitel: 1 Satz, Platzhalter (z.B. „Bald mehr an dieser Stelle.")
- Karten 01/02/03: je ein Titel-Platzhalter + „Under Construction"
- Footer: Ort + Kontakt (Platzhalter)

> Alle Texte als leicht auffindbare Konstanten/Markup, damit Caro sie selbst
> ersetzen kann.

---

## 6. Verhalten

- **Statisch.** Keine Navigation, da alles „in Bau" ist.
- Karten: kein Ziel (oder `href="#"`), dezenter Hover-Effekt.
- Responsive: Desktop = drei Karten nebeneinander; Mobil = gestapelt.
- Video läuft stumm im Loop; Fallback-Hintergrund schwarz, falls Video fehlt.
- Reduced-Motion respektieren (Video ggf. pausieren / statisches Bild).

---

## 7. Dateistruktur (Soll)

```
caro/
├── index.html          # gesamte Seite
├── style.css           # Styling (Schwarz-Weiß)
├── hero-bg.mp4         # ← vom NUTZER hochzuladen (Hintergrundvideo)
├── vercel.json         # Vercel-Konfiguration (statisch)
├── .gitignore
├── README.md
└── SPEC.md             # dieses Dokument
```

> **Wichtig:** Das Video `hero-bg.mp4` lädt der Nutzer selbst ins Repo (Root
> oder `/public`). Im Code wird genau dieser Dateiname referenziert. Fehlt das
> Video, bleibt der Hintergrund schwarz (kein Fehler).

---

## 8. Deployment (GitHub → Vercel)

1. Dateien (inkl. `hero-bg.mp4`) ins GitHub-Repo pushen.
2. Repo auf Vercel importieren. Da statisch: **kein Build-Command**,
   Output = Projekt-Root. `vercel.json` ist enthalten.
3. Jeder Push auf `main` → automatisches Production-Deploy.

---

## 9. Arbeitsanweisung für Claude Code

- SPEC.md ist maßgeblich.
- Schwarz-Weiß strikt einhalten; keine Farben einführen.
- Keine zusätzlichen Abhängigkeiten, kein Build-Tool ohne Not (statisch halten).
- Keine Tracker/Cookies (Datensparsamkeit).
- Videodateiname `hero-bg.mp4` nicht ändern — der Nutzer liefert exakt diese Datei.
- Texte als gut auffindbare Platzhalter belassen, damit Caro sie leicht ersetzt.

---

## 10. Spätere Iterationen

- Echte Inhalte/Titel für 01 / 02 / 03 und Verlinkung der Karten.
- Eigene Unterseiten je Menüpunkt.
- Impressum / Datenschutz ergänzen (rechtlich, sobald live mit Inhalten).
