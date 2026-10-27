# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Personal academic website for Yunfei Zhang (PhD student, Chair of Traffic Engineering and Control, TUM), served by GitHub Pages from the `main` branch. It is a fork of Jon Barron's academic website template (https://jonbarron.info/), and the footer credit to him should stay.

The site is plain static HTML/CSS. There is no build step, package manager, linter or test suite. To preview, open `index.html` in a browser or serve the repo root (e.g. `python -m http.server`). Pushing to `main` deploys.

## Structure

- `index.html` is the entire site. Almost every change is an edit to this one file. It is laid out with nested `<table>`s and inline styles, following the template. Its sections, in order:
  - Header: bio paragraph, contact links, profile photo.
  - **Publications**: grouped by year, newest first. Each year starts with a separator row (`<!-- Separator for year YYYY -->` followed by an `<h3>` row), then has one `<tr>` per paper.
  - **Projects**: research projects, newest first. Each is a linked name followed by funder and duration.
  - **Teaching**: TA semesters list, then supervised Master's and Bachelor's theses, newest first.
  - Footer credit and the ClustrMaps visitor-map script.
- `stylesheet.css`: Lato font faces plus a few classes (`.papertitle`, `.name`, `.one`/`.two` for hover image swaps, `span.highlight`).
- `data/`: per-paper `.bib` files, slides, and `bio_yunfei_zhang.txt`.
- `data/relevant_papers/`: git-ignored local copies of the full-text PDFs plus `0_Summary.xlsx`. Use it as the source for paper metadata and thumbnails, and never commit it.
- The authoritative lists of supervised theses and projects are on the TUM staff page: <https://www.mos.ed.tum.de/en/vt/staff/current/zhang-yunfei/>
- `images/publ/`: one thumbnail per paper. `images/publ/deprecated/` holds old versions that are no longer used.
- `mipnerf/`, `mipnerf360/`, `zipnerf/`: project pages left over from the upstream template. Nothing on the site links to them.

## Conventions

- **Paper key**: `YY_venue_topic`, for example `23_itsc_avaas` or `25_trb_avas_tse`. The same key is used for the thumbnail (`images/publ/<key>.png|jpg`), the bibtex file (`data/<key>.bib`), and the `id` attribute on the paper title's `<a>`.
- **Publication entry**: copy an existing entry inside the right year block. Each entry has:
  - a 160px thumbnail,
  - `<span class="papertitle">` inside the link,
  - an author list where Yunfei is `<strong>Yunfei Zhang</strong>` and co-authors link to their LinkedIn profiles,
  - `<em>VENUE</em>, YEAR` with an optional status such as `(accepted)`, `(presented)` or `(submitted)`,
  - optional links separated by ` / ` (Full paper, bibtex, Poster, Slides),
  - a one-sentence summary starting with "We ...".

  Link slots that are not used yet stay as HTML comments in each entry, so they can be uncommented later.
- **Thesis entry**: a linked title pointing to the TUM thesis PDF (`https://www.mos.ed.tum.de/fileadmin/w00ccp/vt/theses/pdf/{MA|BA}/<year>/...`), then `<br>`, then `Student Name (End: MM/YYYY)`. Entries are separated with `<br>`.
- `index.html` contains large commented-out blocks: template samples (highlighted papers with hover-swap images, a figure row, a text row, a draft Entrepreneurship section) and a TODO list near the top of Publications. Keep them unless asked to remove them; they are reused as references.
- Commit messages use Conventional Commit prefixes (`feat:`, `docs:`, `fix:`, `style:`, `test:`), for example `feat: Add TRB25 AVaS TSE paper.`
