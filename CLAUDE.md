# jonahsworkshop — vibe coding guide

This file documents the conventions of jonahsworkshop.github.io so any AI
assistant (or future me) can add content consistently without re-deriving
the design system.

## Stack & workflow
- Plain HTML, CSS, JS. No build step. No frameworks. No webfonts.
- Hosted on GitHub Pages. Auto-deploys on every commit to `main`.
- Edited via github.dev (press `.` on the repo from github.com).
- Each page is fully self-contained (CSS embedded in `<style>`). No shared
  stylesheet. This is intentional — each page is paste-modify-deploy.

## File structure

    /index.html                       workshop entry (cream + serif)
    /sounds/index.html                brutalist-techno room (black + acid green)
    /sounds/audio/                    self-hosted MP3s
    /writing/index.html               calm room (cream + serif)
    /writing/journal/index.html       poetic room with audio (TBD)
    /recommending/index.html          bookshelf (cream + serif, TBD)
    /recommending/dystopia/index.html dystopian-degraded subpage (TBD)
    /now/index.html                   what i'm doing this month (TBD)
    /colophon/index.html              about the site & me (TBD)
    /CLAUDE.md                        this file

## Design principle: page-as-room
Each section has its own atmosphere driven by its content. Shared bones
(back-link, asymmetric left-leaning layout, .entry component pattern) keep
navigation consistent across rooms. Visitors move between tonally distinct
spaces but never feel lost.

## Aesthetics — three palettes

### Cream-serif (default)
Used on: /, /writing/, /recommending/, /now/, /colophon/
--bg: #f1ece1;    --ink: #2a2520;    --ink-soft: #6b6258;
--accent: #8b3a2a;    --rule: #d8d0c0;
Font: `"Iowan Old Style", "Palatino", Georgia, serif`
Atmosphere: warm, handwritten, calm, hallway-lit

### Brutalist-techno
Used on: /sounds/
--bg: #0c0c0c;    --ink: #e8e8e8;    --ink-soft: #777;
--accent: #9eff5a;    --rule: #222;
Font: `"Berkeley Mono", "JetBrains Mono", "IBM Plex Mono", "Fira Code", Menlo, Consolas, monospace`
Atmosphere: dark, electric, after-midnight, post-rave
Custom JS audio player (no native <audio> visible)

### Dystopian-degraded
Used on: /recommending/dystopia/ (TBD)
Charcoal background, sodium amber accent, mixed mono/serif typography,
subtle CRT/scanline texture. To be designed when the page is built.

## Layout invariants (every page)
- Asymmetric left-leaning content: `margin: 0 auto 0 max(2rem, 12vw)` on `main`
- Max width around 36–44rem
- Back-link at top: `<a class="back" href="/">← back to the workshop</a>`
  (uses room-appropriate styling for the palette)
- `* { box-sizing: border-box; }` reset
- Mobile breakpoint at 600px

## The .entry component
Every content item is `<article class="entry">`. Contains:
- `<h3>` title (optional for very short pieces)
- `<p class="meta">` date · tags · format (italic small grey)
- `<p class="excerpt">` or `<div class="body">` content
- Optional action: `.more`, `.play`, `.ext` button/link

Variants:
- `.entry.with-divider` — dashed bottom border for fragment-length pieces
- Tabular variant on /sounds/ uses `display: grid` with track number column

## How to add content

### Add a sounds track
1. Drop MP3 in `/sounds/audio/`
2. In `/sounds/index.html`, copy an `<article class="entry">` from the
   "making" section. Update the `num`, h3 title, meta spans, note, and
   `data-src` on the play button.
3. Commit. JS picks up new tracks automatically (single-track-at-a-time
   playback works without any JS edits).

### Add a substack post
1. In `/writing/index.html`, copy an `<article class="entry">` from the
   "published" section. Update the link href, title, meta (date + word count),
   tags inside `.tags` div, excerpt, and "read on substack" href.
2. Use 1–3 tags. Common tags: ai, tech, business, music, philosophy.
3. Commit.

### Add a note (from notes app)
1. In `/writing/index.html`, copy an `<article class="entry">` from the
   "notes" section.
2. Use `.entry.with-divider` for fragment-length (1–3 paragraphs). Skip
   the class for single-paragraph musings.
3. Title is optional for short musings; required for fragment-length pieces.
4. Commit.

### Add a workshop door (new section) to the home page
1. In `/index.html`, inside `<nav class="doors">`, copy an `<a>` element.
   Update href, label, and the `<small>` descriptor.
2. Build the corresponding `/folder/index.html` with the back-link to `/`.
3. Commit both files.

## Tone conventions
- Lowercase prose, generally. Title Case where it feels off otherwise.
- Italic small grey for meta and section intros.
- Accent color used sparingly: links, hover states, section headers.
- No emoji in body text. Symbols (`→`, `·`, `←`) are fine.

## Hard rules — do not violate
- No frameworks (no React, no Vue, no Tailwind, no jQuery).
- No webfont requests. System font stacks only.
- No build step. Every page must work as a static HTML file.
- No centered layouts. Content shifts left.
- No native `<audio>` controls visible in brutalist-techno or
  dystopian-degraded palettes — they break the aesthetic. Use custom
  JS players.
