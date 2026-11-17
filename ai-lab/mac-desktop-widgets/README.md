# 🖥️ Mac desktop widgets

📦 **Full project, widget code and a 4-part guide:** [mac-desktop-widgets](https://github.com/Parag-S-Salunkhe/mac-desktop-widgets)

A clean desktop with three text overlays straight on the photo: no cards, just shadowed text on the right edge. Built with [Übersicht](https://tracesof.net/uebersicht/) widgets (JSX) in one afternoon with Claude Code.

| Widget | What it shows |
|---|---|
| **Clocks** | Big local time + two datacentre time zones with sun/moon, 12-hour |
| **System** | Ring gauges for CPU, GPU and memory (app / system / compressed); network ↓↑ with the active interface and link speed; one summary line: pressure · swap · busiest app · biggest-memory app |
| **Free up** | Lists apps by real memory footprint and quits one on click. "Clear swap" appears only when swap is over 1 GB |
| **Wallpaper** | Bing picture of the day in 4K, or a Windows-Spotlight-style shuffle, with a magazine-style caption. Prev / next / favourite, keeps 30 |

**Things I learned**
- `backdrop-filter` blur flickers in Übersicht. Solid gradients don't.
- Disk "free" should be `df` *available* in decimal GB, which matches Finder. Size minus used was 21 GB too optimistic.
- The real battery drain wasn't the widgets (~11 ms CPU every 5 s). It was **System Settings left open on the Wallpaper pane**, which keeps playing aerial previews.
- Write widget files atomically (temp file + rename). A half-written file can freeze the widget engine.
- Security: the widget server answers only on localhost, downloads are HTTPS-only, and file names are sanitised.

**Built with:** Übersicht (JSX), Python, `top` / `netstat` / `scutil`, Claude Code.

[← AI Lab](../README.md)
