# Lonely Binary — Docs

Tutorial content for the [Lonely Binary](https://lonelybinary.com) website.

This repo holds **only MDX content**. The website code lives in the private
`lonely-binary/web` repo and pulls this content in at build time. **You never
need to touch the website code to publish a tutorial** — edit MDX here, push,
and the site rebuilds automatically.

## How publishing works

```
edit .mdx  →  git push (main)  →  GitHub Action pings Vercel  →  site rebuilds
```

A push to `main` triggers `.github/workflows/trigger-rebuild.yml`, which calls a
Vercel deploy hook. The live site updates a minute or two later.

## Folder structure

Tutorials live under `tutorials/`, grouped into category folders. The folder is
just organisation — the **URL comes from the `slug` frontmatter field**, not the
path.

```
tutorials/
  quick-starts/      Short, card-driven tutorials
  communication/     Wi-Fi, BLE, ESP-NOW, MQTT …
  sensors/           ADC, I²C sensors …
  …add categories as needed
```

## Authoring a tutorial

Create a `.mdx` file anywhere under `tutorials/`. Start with frontmatter:

```yaml
---
title: Wi-Fi Connection Manager      # required
slug: wifi-connection-manager        # required — becomes /tutorials/<slug>
category: communication              # required
parent: communication                # optional — for nesting
order: 3                              # optional — sort order (default 100)
level: beginner                       # beginner | intermediate | advanced
estimatedMinutes: 45
authors: [hana]                       # list of author handles
updated: 2026-05-10                    # YYYY-MM-DD
kit: lb-32-starter                     # optional Shopify product handle
tags: [esp32, wifi, comm]
seo:
  description: One-line summary for search engines and link previews.
---
```

Below the frontmatter, write standard Markdown. Two extras are available:

**Callouts** — `<Callout variant="tip">…</Callout>` (`variant` = `info` | `warn`
| `tip`):

```mdx
<Callout variant="warn">
Always set a connection timeout, or the board blocks forever on a bad password.
</Callout>
```

**Code blocks** — fenced blocks are syntax-highlighted. Use `cpp` for
Arduino/C++ and `python` for MicroPython:

````mdx
```cpp
void setup() { Serial.begin(115200); }
```
````

See `tutorials/communication/wifi-connection-manager.mdx` for a complete
example.

> The two flagship tutorials — **ESP-NOW** and the **Bluetooth Quick Start** —
> are currently hand-built in the website repo as pixel-exact designed pages, so
> they are not in this repo yet. Everything else is authored here.
