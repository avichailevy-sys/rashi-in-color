# רש"י בצבעים / Rashi in Color

A proof-of-concept viewer that color-codes Rashi's commentary on **Parashat Ekev** (Deuteronomy 7:12–11:25) by the source each comment draws on, and reconciles two independent source layers against each other — confirming where they agree and surfacing what each one adds.

**Live demo:** https://avichailevy-sys.github.io/rashi-in-color/

---

## What it does

Displays the **standard text of Rashi** on Ekev, comment by comment, and tags each comment from two source layers:

- **Sefaria** — source names spotted in Rashi's text and its English translation.
- **Torat Chaim** — source footnotes from the Mossad HaRav Kook edition, hand-extracted (31 attributions across the parashah).

Each comment gets a reconciliation status:

- **● Confirmed — both** — Sefaria and Torat Chaim name the same source.
- **◐ Both — different source** — both attribute, but to different works.
- **◆ Torat Chaim adds** — a source Sefaria missed (the enhancement).
- **○ Sefaria only** — a source Torat Chaim's footnotes didn't carry.
- **◌ Unattributed** — neither names a source (the residue).

Source chips are tagged by origin, the status pills double as filters, and a **Show details** toggle reveals the precise locus (e.g. *Sifrei Devarim 37*), footnote number, and a confidence flag for each Torat Chaim attribution.

## Data sources

Rashi's text and the Sefaria layer are fetched live from the [Sefaria API (v3)](https://developers.sefaria.org/reference/get-v3-texts) at page load. The Torat Chaim layer is embedded in the page (also published as `torat-chaim-ekev-sources.csv` / `.json`), extracted from the printed edition's source footnotes — keeping only genuine source attributions and dropping explanatory glosses (Maharik, Mizrachi, cross-references).

## Why two layers

Sefaria has no structured source data for Rashi here, so its layer only catches a source when a name happens to appear in the prose — incidental and incomplete. Torat Chaim records the source as a real editorial note on the comment, so it recovers attributions Sefaria misses (on Ekev, most of them: the Sifrei spine of chapter 11, the Mekhilta/Tanchuma on 10:6, the Bezalel-ark cluster on 10:1). The viewer makes that comparison visible: agreement is confirmation, divergence is enhancement.

## Known limitations

- The Torat Chaim attributions were read from photographs of the printed edition; medium- and low-confidence loci are flagged and should be spot-checked against the book before citation.
- Sefaria–Torat Chaim alignment matches by verse plus the opening words of the dibbur. It is deliberately conservative — records whose dibbur doesn't line up are listed separately as "not auto-aligned" rather than forced onto the wrong comment.
- This covers one parashah and one witness (standard Rashi). It demonstrates the method, not a complete apparatus.

## Roadmap

- An **Al HaTorah** version, pointed at the Al HaTorah witness with its systematic *מקור* links.
- A **TR-tool layer** (ACT, passim, Dicta) to detect *paraphrastic* reuse, where Rashi reworks a source without naming it.
- Reconciliation across scholarship and automated tools together, in the GenizaNexus pattern.

## Running locally

The page fetches from Sefaria at runtime, so it must be **served**, not opened from disk:

```bash
python3 -m http.server 8000
```

then open `http://localhost:8000/`. Over https (GitHub Pages, Netlify) it works with no extra steps.

## Built with

A single `index.html` — React + Babel from CDN, no build step.

## Context

Part of ongoing research on mapping Rashi's commentary to its rabbinic sources, within the MiDRASH project (Tel Aviv University / University of Haifa).

<!-- Acknowledgments / collaborators: add as you see fit. -->
