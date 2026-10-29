# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Personal website (yera.dev) styled as a terminal window. It is a static site: three standalone HTML files plus `favicon.png`. There is no build step, package manager, linter, or test suite. To preview, open `index.html` in a browser or run `python3 -m http.server`.

## Architecture

- `index.html` is the landing page. Each terminal line is a `<div class="line" id="lN">` that is hidden by default (`display: none`) and revealed by the inline `<script>` at the bottom. That script holds a `schedule` array of `[lineId, delayMs]` pairs, and a `setTimeout` adds the `visible` class to each line. **When adding or removing a line, renumber the `id`s and update `schedule` to match**, or the line never appears.
- `experience.html` is the experience and education page. It has no JavaScript. Entries (`.job`, `.edu-entry`) animate in with a CSS `fadeUp` animation and per-`nth-child` `animation-delay` rules. Adding more than 5 jobs or 2 education entries needs new `nth-child` delay rules.
- `memento-mori.html` is a calculator page: date of birth and life expectancy go in, and the time left (years, months, weeks, days) comes out. Its inline script recomputes on every input and remembers the last inputs in `localStorage`. It is deliberately unlisted: it is not linked from any page (only reachable by its URL) and carries a `noindex, nofollow` robots meta tag. Don't add a link to it.
- Each page inlines its own `<style>` block. Styles are duplicated, not shared, so a theme change has to be made in both files. The theme is a dark background (`#0d0d0d`) with a Courier New monospace font. Pages are linked with plain relative `href`s.
- Both pages share the same footer text, aimed at AI crawlers. Keep it in sync across pages.
- `.gitignore` only excludes `sbr-converter.tar`.
