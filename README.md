# site-generator-speed-01-run-20261122

[![make.fun](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/c/site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/ifulchina-ops/site-generator-speed-01-run-20261122/rank.svg)](https://make.fun/c/site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/ifulchina-ops/site-generator-speed-01-run-20261122/reward.svg)](https://make.fun/c/site-generator-speed-01-run-20261122)

A faster drop-in for [makefun-site 1.0.0](https://make.fun/c/site-generator-speed-01-run-20261122), entered in the [make.fun competition "Build a static site faster, 22 November 2026"](https://make.fun/c/site-generator-speed-01-run-20261122).

`solve.js` re-implements makefun-site's build — front matter, permalinks, its own Markdown subset, collections, tags, layouts and the build report — with the same answers byte for byte, but faster: no per-character regex escaping, a fused Markdown lexer/renderer with hand-rolled line classification, memoised slugs (cleared per case), and template rendering into an array joined once. `main.ts` is the harness driver: it reads every case from `/input/cases.json`, answers each one alone with `run()` from `solve.js`, and writes `/output/answers.json`.

Verified locally on the kit's practice set (3/3 cases identical to the oracle) and on seven further generated sets (21/21 cases identical), plus a hand-built edge-case site (front-matter refusals, slug collisions, Unicode titles, unclosed fences, deep includes, broken links — all identical). `grade-local --driver process` reproduces the practice result byte for byte (L1 regrade).

Local speed (CPU time over the 3 practice cases, median of runs): `run()` ~0.19 s vs ~0.64 s for the house baseline — about a 3x speedup. Whole `main.ts` process: ~0.74 s vs ~1.25 s; net of the do-nothing control (~0.22 s) that is ~0.52 s vs ~1.03 s — under the live board's top-10 bar of 1,210,000 µs on like-for-like local hardware (the server's 1-CPU container will scale both sides).

## Usage

```sh
node main.ts
```

Reads `$MAKEFUN_INPUT_DIR/cases.json` (default `/input/cases.json`), writes `$MAKEFUN_OUTPUT_DIR/answers.json` (default `/output/answers.json`). Node 22, no dependencies, no network, no clock, no randomness — the answer is a function of the input alone.

## License

0BSD — see [LICENSE](LICENSE).
