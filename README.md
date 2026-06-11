# רש"י בצבעים / Rashi in Color

A proof-of-concept viewer that color-codes Rashi's commentary on **Parashat Ekev** (Deuteronomy 7:12–11:25) by the source each comment draws on — and highlights what is left unattributed as the "original Rashi" layer.

**Live demo:** https://avichailevy-sys.github.io/rashi-in-color/

---

## What it does

- Displays the **standard text of Rashi** on Ekev, in Hebrew (RTL), comment by comment.
- **Colors each comment by its source** — Midrash Tanchuma (green), Sifrei, Sifra / Torat Kohanim, Mekhilta, Yerushalmi, Talmud Bavli, Targum / Onkelos, Midrash Rabbah.
- Marks comments with **no detected source** as *"original Rashi"* (dashed, neutral) — the residue the project is ultimately interested in.
- **Filter** by source, **isolate the residue** with one toggle, and open the **match-basis panel** to audit exactly which word triggered each color and where it appeared.

## Data source

Text and translation are fetched live from the [Sefaria API (v3)](https://developers.sefaria.org/reference/get-v3-texts) — the standard Hebrew Rashi plus its English translation — at page load. Nothing is stored; the page is a single static file.

## Important limitation

This is a demonstration of the **interface**, not a finished source apparatus.

Sefaria does not hold Rashi's sources as structured data for this text — there are no source footnotes in the API response. Attribution here therefore works by **keyword-matching** source names against Rashi's text and its English translation. That catches a source only when it happens to be named in passing, so coverage is **incidental and incomplete**, and the residue is correspondingly inflated. Read the colors as a working prototype of how a real attribution layer would look, not as an authoritative claim about Rashi's sources.

## Roadmap

- **Al HaTorah version** — repoint the same viewer at the Al HaTorah witness, whose per-comment *מקור* links are systematic rather than incidental, and compare the two side by side. (Next step.)
- **TR-tool layer** — bring in ACT, passim, and Dicta to detect *paraphrastic* reuse, where Rashi reworks a source rather than naming it — the hard "מעבד" cases that keyword-matching and verbatim alignment both miss.
- **Reconciliation view** — agreement / disagreement across scholarship and the automated tools, in the GenizaNexus pattern.

## Running locally

Because the page fetches from Sefaria at runtime, it must be **served**, not opened directly from disk (a `file://` page will be blocked from making the request). From the project folder:

```bash
python3 -m http.server 8000
```

then open `http://localhost:8000/`. Served over https (GitHub Pages, Netlify), it works with no extra steps.

## Built with

A single `index.html` — React + Babel loaded from CDN, no build step.

## Context

Part of ongoing research on mapping Rashi's commentary to its rabbinic sources, within the MiDRASH project (Tel Aviv University / University of Haifa).

<!-- Acknowledgments / collaborators: add as you see fit. -->
