# ScanMagic

A mobile-first **document scanner** that runs entirely in the browser — no install, no server, no account.

Open `scanner.html` on your phone or desktop and scan like Adobe Scan: capture, flatten, clean, OCR, multi-page PDF.

![License](https://img.shields.io/badge/license-MIT-blue)
![Platform](https://img.shields.io/badge/platform-Web-green)
![Offline-capable](https://img.shields.io/badge/processing-client--side-orange)

## Features

### Capture
| Mode | Best for |
|------|----------|
| **Document** | Contracts, letters, forms |
| **Receipt** | Expense receipts & invoices |
| **Business Card** | Contact cards + OCR |
| **Whiteboard** | Meeting notes & boards |
| **Photo** | Existing gallery images |

- Rear camera preferred (with front/rear switch)
- Import from gallery
- Responsive mobile UI with safe-area support

### Image processing
- **Flatten** — perspective correction (tap 4 corners, drag to adjust)
- **Crop** & **Rotate**
- **Auto Fix** — clean shadows / edge gradients while **keeping text dark**
- **Heal** — fill **folds & tears** with matching paper color
- **Magic Eraser** — content-aware brush (samples surrounding background)
- **Deblur** — unsharp mask tuned for printed/handwritten text
- **Filters** — Original, Enhance, Grayscale, B&W, High Contrast, Whiteboard
- **Markup** — draw annotations (multiple colors + pen size)
- **Undo** (multi-step) & Reset

### OCR & export
- **OCR** — extract text with [Tesseract.js](https://tesseract.projectnaptha.com/) (copy to clipboard)
- **Multi-page** — add pages to a session, then export together
- **JPEG** export with quality control (High / Medium / Small)
- **PDF** export via [jsPDF](https://github.com/parallax/jsPDF) (single or multi-page)
- Optional page size estimate after flatten (A4, Letter, etc.)

## Quick start

1. Clone or download this repo.
2. Open `scanner.html` in a modern browser  
   - **Phone:** Safari / Chrome (HTTPS or `localhost` required for camera)  
   - **Desktop:** any Chromium/Firefox/Safari build
3. Allow camera access when prompted.
4. Pick a scan mode → **Scan** or **From Gallery**.

```bash
# optional: serve locally so camera works reliably
npx serve .
# then open the printed URL on your phone
```

> **Note:** First OCR run downloads language data (needs network once). Core editing works offline after the page is loaded.

## Suggested workflow

1. Choose a **mode** (Document, Receipt, …)
2. Capture or pick a photo
3. **Flatten** — tap the four corners of the page → Apply
4. **Auto Fix** → **Heal** (if folds/tears) → **Deblur**
5. **Magic Eraser** / **Markup** for leftovers
6. **＋ Page** for additional pages
7. **OCR** if you need text · **Export** → JPEG or PDF

## Tech stack

| Piece | Detail |
|-------|--------|
| UI | Single HTML file, CSS, vanilla JS |
| Camera | `getUserMedia` |
| Processing | Canvas 2D / `ImageData` (no WebGL required) |
| OCR | Tesseract.js 5 (CDN) |
| PDF | jsPDF 2.x (CDN) |

No build step. No backend. All heavy lifting stays on the device.

## Browser support

- Chrome / Edge (Android & desktop) — recommended  
- Safari iOS 15+  
- Firefox recent  

Camera and clipboard require a [secure context](https://developer.mozilla.org/en-US/docs/Web/Security/Secure_Contexts) (`https://` or `http://localhost`).

## Project layout

```
├── scanner.html   # full app (UI + logic)
└── README.md
```

## Limitations (honest)

These are hard or impossible in pure client-side JS without large models:

- Live auto edge-detection / auto-shutter on the camera viewfinder  
- Cloud sync or Adobe account features  
- PDF/A archival compliance  
- True generative “content-aware fill” (Heal approximates with local paper sampling)  
- Editable OCR text embedded as vectors in the PDF (text is available via the OCR panel)

## Privacy

Images never leave your device unless **you** export/share them. OCR language packs are fetched from the Tesseract CDN on first use; recognition itself runs locally.

## License

MIT — use, copy, modify, ship freely.

---

Built as a lightweight, private alternative to commercial phone scanners.
