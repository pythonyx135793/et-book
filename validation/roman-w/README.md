# Roman w rendering evidence

Application: `70dc08310c5bbe065af66f381b34bc9b35cd0684`.
Original: `24d3a3bbfc880095d3df2b9e9d60d05819138e89`.

The Roman LF and OSF lowercase `w` is too tall at 12, 17 and 22px in the original fonts. The repair anchors the top serif to the existing x-height control value. Only that glyph's instructions change.

- Native Windows GDI: 20,038 glyph/size comparisons over all 233 glyphs in both fonts at 8–48, 64 and 96px. All non-`w` bitmaps/metrics and all advances are identical. All six original height mismatches are corrected.
- [Linux result](https://github.com/pythonyx135793/et-book/actions/runs/40148331690/job/121034377736): nine structural/rebuild tests and 40,076 actual FreeType comparisons pass with interpreters 35/40. All 36 paired original-failure/fixed-pass height controls pass at coverage 32/128/224. Raw non-`w` pixels and metrics remain identical.
- Windows Chromium 155: original/fixed TTF and WOFF comparisons for both fonts. Passive font-request receipts identify all eight exact font files. Browser screenshots supplement the native raster checks; they are not all-browser coverage.

## Native-resolution overlays

Red is **excess original coverage**; black is the fixed glyph. Shared coverage is removed from red so identical antialiased pixels do not create a false fringe. Open each PNG at 100% to inspect native pixels. No glyph scaling was used. All-glyph sheets show 233 defined glyphs at 64px, including `g`, `e` and capital `W`.

| Font | 12–32px comparison | All glyphs at 64px |
| --- | --- | --- |
| Roman LF | [Overlay](native-roman-lf-overlay.png) | [All glyphs](native-roman-lf-all-glyphs.png) |
| Roman OSF | [Overlay](native-roman-osf-overlay.png) | [All glyphs](native-roman-osf-all-glyphs.png) |

Browser captures: [LF TTF](browser-roman-lf-ttf.png), [LF WOFF](browser-roman-lf-woff.png), [OSF TTF](browser-roman-osf-ttf.png), [OSF WOFF](browser-roman-osf-woff.png). These show original, fixed and a conventional red-under-black browser overlay. The small left-hand size/row labels overlap in this proof page; the native PNGs above provide the precise keyed comparisons.

At 20px, the corrected `w` retains its dimensions and advance but has small antialias differences. EOT metadata and its exact fixed-TTF payload are structurally checked; legacy IE rendering is untested. Healthy source fonts, other styles and ligature-enabled fonts remain unchanged.

The first Linux run passed structure checks but exposed an invalid test assumption: bitmap allocation bounds include fully transparent rows or tiny fringes. The corrected test checks visible edges at three explicit coverage levels, retaining strict raw bitmap equality for unrelated glyphs. Both original and final logs are preserved. No font change was made in response to that harness failure.

`manifest.json` records the evidence files; `source-manifest.json` records the exact ten application files. `provenance.json`, `windows-result.json`, `linux-result.json` and the raw logs give methods, versions, hashes and limits. The application's `source/hinting` directory contains the rebuild and Linux raster checks.
