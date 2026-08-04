<p align="center"><img src="https://raw.githubusercontent.com/go-webengine/brand/main/social/go-webengine.png" alt="go-webengine" width="720"></p>

<h1 align="center">go-webengine</h1>
<p align="center">A pure-Go (CGO=0) headless web engine — give it a URL, get back an image of the page. No Chromium, no cgo.</p>
<p align="center">[![site](https://img.shields.io/badge/site-go--webengine.github.io-0079A8?style=flat-square)](https://go-webengine.github.io/) [![docs](https://img.shields.io/badge/docs-mkdocs--material-0A6E96?style=flat-square&logo=materialformkdocs&logoColor=white)](https://go-webengine.github.io/docs/) ![repos](https://img.shields.io/badge/repos-1-0079A8?style=flat-square) ![Go](https://img.shields.io/badge/Go-1.26.4%2B-00ADD8?style=flat-square&logo=go&logoColor=white) ![license](https://img.shields.io/badge/license-BSD--3--Clause-0A6E96?style=flat-square)</p>

---

## What is this?

`go-webengine` renders web pages **in pure Go**. It fetches a URL, parses the
HTML into an owned DOM, applies a minimal-but-real CSS cascade (specificity +
inheritance), lays the content out in block-and-inline flow, and paints
anti-aliased text, backgrounds and images to an `image.RGBA` → PNG — **no
Chromium, no cgo, no host web view**. One static binary, identical on every OS.

```go
png, _ := engine.Screenshot(ctx, "https://example.com/", image.Rect(0, 0, 1024, 768))
os.WriteFile("out.png", png, 0o644)
```

It is the rendering core of the [wasmdesk](https://github.com/wasmdesk)
**browserproxy** roadmap. Phase 0 — shipping today — is a *static* renderer (no
JavaScript); what works and what does not is documented honestly in the engine's
[fidelity report](https://github.com/go-webengine/engine/blob/main/FIDELITY.md).

## Repositories (1)

| Module | Kind | What it is | API |
|---|---|---|:--:|
| [`engine`](https://github.com/go-webengine/engine) | lib + cli | Fetch → DOM → CSS cascade → block/inline layout → paint to `image.RGBA` / PNG. Pure Go, CGO=0. Ships a `render` CLI. | [ref](https://pkg.go.dev/github.com/go-webengine/engine) |

> This list reflects the repos that actually exist in the org.

## Roadmap

- **Phase 0 — static renderer · shipping.** HTML/CSS cascade, block/inline flow, AA text/background/image paint. No JS.
- **Phase 1 — scripting · planned.** A pure-Go JS engine ([goja](https://github.com/dop251/goja)) wired to the DOM.
- **Phase 2 — real box model · planned.** float / flex / grid / table layout and positioning.
- **Phase 3 — browserproxy · planned.** Render server-side, stream frames to the wasmdesk `clients/browser`.

## Links

- 🌐 Site — <https://go-webengine.github.io/>
- 📖 Docs — <https://go-webengine.github.io/docs/>
- 🎨 Brand assets — <https://github.com/go-webengine/brand>

---
<p align="center"><sub>Branding in <a href="https://github.com/go-webengine/brand">go-webengine/brand</a>.</sub></p>
