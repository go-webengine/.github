<p align="center"><img src="https://raw.githubusercontent.com/go-webengine/brand/main/social/go-webengine.png" alt="go-webengine" width="720"></p>

<h1 align="center">go-webengine</h1>
<p align="center">A pure-Go (CGO=0) headless web engine — give it a URL, get back an image of the page. No Chromium, no cgo.</p>
<p align="center">
  <a href="https://go-webengine.github.io/"><img src="https://img.shields.io/badge/site-go--webengine.github.io-0079A8?style=flat-square" alt="site"></a>
  <a href="https://go-webengine.github.io/docs/"><img src="https://img.shields.io/badge/docs-mkdocs--material-0A6E96?style=flat-square&logo=materialformkdocs&logoColor=white" alt="docs"></a>
  <img src="https://img.shields.io/badge/repos-2-0079A8?style=flat-square" alt="repos">
  <img src="https://img.shields.io/badge/Go-1.26.4%2B-00ADD8?style=flat-square&logo=go&logoColor=white" alt="Go 1.26.4+">
  <img src="https://img.shields.io/badge/license-BSD--3--Clause-0A6E96?style=flat-square" alt="license BSD-3-Clause">
</p>

---

## What is this?

`go-webengine` renders web pages **in pure Go**. It fetches a URL, parses the
HTML into an owned DOM, applies a real CSS cascade (specificity + inheritance +
`var()` + dark-mode), **runs the page's JavaScript** against a real DOM, lays the
content out with a full box model (block, inline, float, flex, grid, table,
`position`), and paints anti-aliased text, gradients, images and SVG to an
`image.RGBA` → PNG — **no Chromium, no cgo, no host web view**. One static binary,
identical on every OS.

```go
png, _ := engine.Screenshot(ctx, "https://example.com/", image.Rect(0, 0, 1024, 768))
os.WriteFile("out.png", png, 0o644)
```

It is the rendering core of the
[`browserproxy`](https://github.com/go-webengine/browserproxy) remote-browser
service and the [wasmdesk](https://github.com/wasmdesk) in-desktop browser. It is
**not** a Chromium replacement and not claimed to match it pixel-for-pixel:
`example.com` renders at near-parity (0.954 SSIM, ~35× faster), while JS-heavy and
large computed pages are the honest frontier (mean SSIM ≈ 0.69). What works and
what does not is documented honestly, measured against headless Chrome, in the
engine's [fidelity report](https://github.com/go-webengine/engine/blob/main/FIDELITY.md)
and [benchmark](https://github.com/go-webengine/engine/blob/main/bench/REPORT.md).

## Repositories (2)

| Module | Kind | What it is | API |
|---|---|---|:--:|
| [`engine`](https://github.com/go-webengine/engine) | lib + cli | Fetch → DOM → CSS cascade → JavaScript → full box-model layout → paint text/gradients/images/SVG to `image.RGBA` / PNG. Pure Go, CGO=0. Ships a `render` CLI. | [ref](https://pkg.go.dev/github.com/go-webengine/engine) |
| [`browserproxy`](https://github.com/go-webengine/browserproxy) | cli | Remote-browser WebSocket service: renders server-side with the engine, streams frames + a click hit-map to a thin client, forwards clicks/scrolls/keys. SSRF-guarded. | [ref](https://pkg.go.dev/github.com/go-webengine/browserproxy) |

> This list reflects the repos that actually exist in the org.

## Roadmap

Phases 0 through 2.4 have shipped, and the browserproxy remote-browser service is
live. See the engine's
[fidelity report](https://github.com/go-webengine/engine/blob/main/FIDELITY.md) for
the phase-by-phase log.

- **Static render + full box model · shipping.** HTML/CSS cascade, block/inline flow, floats, flexbox, CSS grid, tables and `position`.
- **CSS breadth + SVG · shipping.** `var()`, `@media`, dark-mode, modern colour, gradients, `background-image`, border-radius, box-shadow, opacity, and pure-Go SVG.
- **JavaScript + dynamic render · shipping.** [goja](https://github.com/dop251/goja) + real DOM + `fetch()`/XHR + a settle-then-render loop; sibling combinators, `:checked`, `:not()`.
- **browserproxy · shipping.** Render server-side, stream frames to the wasmdesk `clients/browser`.
- **Remaining levers · planned.** List markers, icon fonts, `conic-gradient`/`filter`/`mask`, SVG filters, and the perf gap on large computed pages — diminishing returns.

## Links

- 🌐 Site — <https://go-webengine.github.io/>
- 📖 Docs — <https://go-webengine.github.io/docs/>
- 🎨 Brand assets — <https://github.com/go-webengine/brand>

---
<p align="center"><sub>Branding in <a href="https://github.com/go-webengine/brand">go-webengine/brand</a>.</sub></p>
