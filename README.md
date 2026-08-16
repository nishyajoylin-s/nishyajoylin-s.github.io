# nishyajoylin-s.github.io

Personal portfolio site. Plain static HTML and CSS — no build step, no framework,
no runtime dependencies. GitHub Pages serves `main` at the repo root.

Live at `https://nishyajoylin-s.github.io/`

## Structure

```
nishyajoylin-s.github.io/
├── index.html   # Single-page portfolio: work, experience, skills, writing, about, contact
├── blog.html    # Essays
├── site.css     # Design tokens + shared styles for both pages
└── assets/      # Hero animation frames (WebP) + social preview image
```

`index.html` carries its layout in inline styles and its ~120 lines of behaviour
(scroll reveal, progress bar, hero frame animation, parallax) in one script at the
end of the file. Shared things — colour tokens, hover/focus states, responsive
rules, blog typography — live in `site.css`.

The page was designed as a Claude artifact and then converted to static HTML: the
original export needed React, ReactDOM and Babel from a CDN at page load, which
meant a blank page for anyone whose network or search crawler could not reach it.
The untouched export is archived outside this repo at `../portfolio-sage/`.

## Hero animation

15 WebP frames in `assets/`: `wave-f0..f7` (waving loop), `trans-f0..f2` (lowering
the hand), `work-f0..f3` (settling into typing). A 90 ms interval walks the strip;
scrolling past 150px flips it from waving to working and back. Frozen on frame 0
for anyone with `prefers-reduced-motion: reduce`.

The frame PNGs are the original artwork, byte-for-byte as exported. Keep them
that way — re-encoding them has been tried and rejected. If you ever need to
touch them, the export is archived at `../portfolio-sage/`.

The only JS additions over the original are three guards, none of which change
the animation itself:

- the loop waits for every frame to decode before starting;
- it never swaps onto a frame that has not loaded yet;
- it holds on `wave-f0` until the hero's entrance animation finishes. The hero
  fades in over ~1.25s (0.35s delay + 0.9s `rise`), and the original started
  waving during that fade, so she materialised mid-flap — that was the flicker
  on first load.

## Local preview

```
python3 -m http.server 8000
```

Then open `http://localhost:8000`. Opening `index.html` from the filesystem works
too, but the embedded Streamlit apps behave better over HTTP.

## Adding a post

Copy an existing `.card` block in `blog.html`, put it at the top (newest first),
and give it a unique `id` so `index.html` can deep-link to it from the writing
section.

## License

Personal use only. All rights reserved.
