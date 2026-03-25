# root@HIVE

**[hive.scyne.com](https://hive.scyne.com)**

Personal server index for `HIVE`. The landing page displays live server uptime alongside a full-screen Matrix digital rain effect. Error pages and tooling are documented below.

---

## Index

The root [`https://hive.scyne.com`](https://hive.scyne.com) serves a live uptime display layered over a Matrix code rain effect. The effect is built on [REGL](https://regl.party) and runs entirely in the browser with no additional setup.

The uptime widget in the bottom-right corner fetches live data from the `n8n.hive.scyne.com/webhook/server-uptime` endpoint and refreshes every 60 seconds.

### Matrix Modes

Append URL parameters to switch between effect variants:

| Mode | URL |
|------|-----|
| Classic | [`hive.scyne.com`](https://hive.scyne.com) |
| 3D | [`hive.scyne.com/?version=3d`](https://hive.scyne.com/?version=3d) |
| Operator | [`hive.scyne.com/?version=operator`](https://hive.scyne.com/?version=operator) |
| Resurrections | [`hive.scyne.com/?version=resurrections`](https://hive.scyne.com/?version=resurrections) |
| Megacity | [`hive.scyne.com/?version=megacity`](https://hive.scyne.com/?version=megacity) |
| Trinity | [`hive.scyne.com/?version=trinity`](https://hive.scyne.com/?version=trinity) |
| Nightmare | [`hive.scyne.com/?version=nightmare`](https://hive.scyne.com/?version=nightmare) |
| Paradise | [`hive.scyne.com/?version=paradise`](https://hive.scyne.com/?version=paradise) |
| Palimpsest | [`hive.scyne.com/?version=palimpsest`](https://hive.scyne.com/?version=palimpsest) |
| Twilight | [`hive.scyne.com/?version=twilight`](https://hive.scyne.com/?version=twilight) |
| Morpheus | [`hive.scyne.com/?version=morpheus`](https://hive.scyne.com/?version=morpheus) |
| Bugs | [`hive.scyne.com/?version=bugs`](https://hive.scyne.com/?version=bugs) |
| Mirror (with camera) | [`hive.scyne.com/?version=updated&effect=mirror&camera=true`](https://hive.scyne.com/?version=updated&effect=mirror&camera=true) |
| Mirror (without camera) | [`hive.scyne.com/?version=updated&effect=mirror`](https://hive.scyne.com/?version=updated&effect=mirror) |
| Pride | [`hive.scyne.com/?effect=pride`](https://hive.scyne.com/?effect=pride) |
| Trans | [`hive.scyne.com/?effect=trans`](https://hive.scyne.com/?effect=trans) |
| Blank intro | [`hive.scyne.com/?skipIntro=false`](https://hive.scyne.com/?skipIntro=false) |

### Effect Parameters

All parameters can be chained with `&`:

```
https://hive.scyne.com/?numColumns=100&fallSpeed=-0.1&slant=200
```

| Parameter | Description | Default |
|-----------|-------------|---------|
| `version` | Effect variant (see table above) | `classic` |
| `skipIntro` | Start from blank screen | `true` |
| `font` | Glyph set (`matrixcode`, `resurrections`, `gothic`, `coptic`, `huberfishA`, `huberfishD`) | `matrixcode` |
| `numColumns` | Number of columns/rows | `80` |
| `animationSpeed` | Overall animation speed | `1.0` |
| `fallSpeed` | Rain descent speed | `1.0` |
| `cycleSpeed` | Glyph cycling speed | `1.0` |
| `raindropLength` | Vertical scale of raindrops | — |
| `slant` | Angle of descent in degrees | `0` |
| `bloomSize` | Glow radius, 0–1 | `0.4` |
| `bloomStrength` | Glow intensity, 0–1 | `0.7` |
| `resolution` | Render resolution relative to window | `1` |
| `glyphRotation` | Per-glyph rotation in degrees | `0` |
| `glyphFlip` | Flip glyphs | `false` |
| `volumetric` | Render with depth (3D) | `false` |
| `density` | 3D raindrop count multiplier | `1.0` |
| `forwardSpeed` | 3D raindrop approach rate | `1.0` |
| `effect` | Post-processing (`plain`, `pride`, `stripes`, `image`, `mirror`, `none`) | — |
| `camera` | Enable webcam input for mirror effect | `false` |
| `stripeColors` | Stripe colors as `R,G,B,R,G,B,...` | — |
| `palette` | Color grade as `R,G,B,%,...` | — |
| `backgroundColor` | Background color as `R,G,B` | — |
| `cursorColor` | Cursor color as `R,G,B` | — |
| `glintColor` | Glint color as `R,G,B` | — |
| `cursorIntensity` | Cursor glow brightness | `2.0` |
| `glintIntensity` | Glint glow brightness | `1.0` |
| `url` | Image URL for `effect=image` | — |
| `fps` | Framerate cap, 0–60 | `60` |
| `ditherMagnitude` | Pixel darkening to reduce banding | `0.05` |
| `suppressWarnings` | Suppress GPU warnings | `false` |

---

## Error Pages

HTTP errors are served as styled glitch pages using the Silkscreen font and a scanline overlay. All three error pages share the same `glitch.css` and `js/main.e.js` assets.

| Error | Path | Description |
|-------|------|-------------|
| `404` | `/404.html` | Not Found |
| `500` | `/500.html` | Internal Server Error |
| `502` | `/502.html` | Bad Gateway |

Each page renders a full-screen glitch treatment of the error code over a black canvas background, with the Matrix rain running underneath.

---

## Tools

### LoRA-Jack

**[hive.scyne.com/sidewalk/lorajack](https://hive.scyne.com/sidewalk/lorajack)**

Signal telemetry dashboard for the Sidewalk Test Kit — a LoRa-LDR field device. Displays live ping data from an n8n webhook, plots the 48-hour GPS trail on a dark tile map, and highlights the most recent ping location with a pulsing marker.

Features:
- Most recent ping highlighted on map (white pulsing dot)
- Last 30 minutes of pings shown in electric blue
- Full ping history accessible via modal
- Live SNR, connection status, and GPS coordinate readout
- Auto-centers map on latest known position on each refresh

---

## Repo Structure

```
/
├── index.html          # Server landing page (uptime + Matrix effect)
├── 404.html            # Not Found error page
├── 500.html            # Internal Server Error page
├── 502.html            # Bad Gateway error page
├── glitch.css          # Shared glitch/scanline styles for error pages
├── assets/             # Matrix glyph fonts and textures
├── js/
│   ├── main.js         # Matrix effect entry point (index)
│   └── main.e.js       # Matrix effect entry point (error pages)
└── sidewalk/
    └── lorajack/       # LoRA-Jack telemetry dashboard
```

---

## Credits

Matrix digital rain effect originally developed by [Rezmason](https://github.com/Rezmason/matrix), built on [REGL](https://regl.party). Glyph vectors sourced from archived promotional material for official Matrix products. Coptic glyphs derived from [George Douros's Symbola](http://users.teilar.gr/~g1951d). Gothic glyphs derived from [Robert Pfeffer's Silubur](http://www.robert-pfeffer.net/gotica/englisch/index.html). Huberfish glyphs by [Teague Chrystie](http://robotsoup.com/huberfish.html).