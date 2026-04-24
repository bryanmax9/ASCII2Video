# ASCII2Video

Convert any video file into animated ASCII art — entirely in your browser. No uploads, no servers, no dependencies.

## Demo

Drop a video, tune the settings, and watch it render as glowing terminal characters in real time.

## Features

- **Drag & drop** `.mp4`, `.mov`, `.webm`, `.avi`, `.mkv` (up to 200 MB)
- **5 detail levels** — Outline → Ultra (40–180 columns)
- **6 character styles** — Classic, Retro, Blocks, Minimal, Digital, Braille
- **4 playback speeds** — 5 / 10 / 20 / 30 fps
- **Brightness mode** — darks filled or lights filled (invert)
- **Live color picker** — Green, Blue, Pink, White
- **Export options**
  - Download as `.webm` video (screen-recorded)
  - Copy self-contained HTML embed snippet
  - Download raw frame data as JSON

## How It Works

1. **Drop video** — file stays local, never leaves the device
2. **Frame sampling** — each frame is drawn to an off-screen `<canvas>` and pixel data is extracted
3. **Luminance mapping** — brightness computed via ITU-R BT.601: `0.299R + 0.587G + 0.114B`
4. **Character mapping** — luminance value indexes into a density ramp (e.g. ` .'^\`,:;Il!i><~+...@$`)
5. **Playback** — frames animate at the selected FPS using `setInterval`

## File Structure

```
ASCII2Video/
├── index.html   # markup
├── styles.css   # all styles and animations
├── main.js      # conversion algorithm, playback, export, UI logic
└── README.md
```

## Usage

Open `index.html` in any modern browser — no build step needed.

```bash
# Quick local server (optional, avoids file:// quirks)
npx serve .
# or
python3 -m http.server
```

Then open `http://localhost:3000` (or `8000`).

## Algorithm

Character sets are defined as density ramps ordered light → dense:

| Style   | Characters |
|---------|-----------|
| Classic | ` .'^\`,:;Il!i><~+_-?][}{1)(|/tfjrxnuvczXYUJCLQ0OZmwqpdbkhao*#MW&8%B@$` |
| Retro   | ` .:-=+*#%@` |
| Minimal | ` .:*#@` |
| Blocks  | ` ░▒▓█` |
| Digital | ` .01` |
| Braille | ` ⠁⠃⠇⠗⠷⠿⣿` |

Font aspect ratio (`FONT_RATIO = 0.44`) corrects the row height so ASCII frames aren't vertically stretched.

## License

MIT
