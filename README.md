# idcopy — certified document copy generator (สร้างสำเนาเอกสารพร้อมข้อความคาด)

A single-page tool for producing a print-ready A4 sheet from a photo or scan of an
identity document, with a diagonal purpose band written across the image — the
standard Thai practice for a certified copy (สำเนาถูกต้อง), and what the PDPA
(พ.ร.บ. คุ้มครองข้อมูลส่วนบุคคล พ.ศ. 2562) expects: state the purpose on the copy so
it cannot be reused for anything else.

**Live:** https://bakatest-me.github.io/idcopy/

## Privacy

Nothing leaves the browser. There is no server, no analytics, no external
library, and no CDN request.

- The dropped image is read with `FileReader`, drawn to a `<canvas>`, and never sent anywhere.
- The PDF is assembled byte by byte in JavaScript (a single JPEG XObject in a minimal
  PDF 1.4 container) — no PDF library is loaded.
- A `Content-Security-Policy` meta tag sets `default-src 'none'`, which blocks every
  network request the page could otherwise make.
- `localStorage` holds layout settings only (angle, opacity, font size, band position,
  image width, title, band text, footer text). The certifier name is deliberately
  excluded, and the image is never stored.

Because the whole app is one file, you can also save it and run it offline: open
`index.html` from disk with no network connection at all.

## Usage

1. Drop an image on the left panel — drag and drop, click to browse, or paste with `Ctrl`/`Cmd`+`V`.
2. Type the purpose of the copy, or pick one of the presets (resignation and share
   transfer, job application, bank transaction, government office).
3. Adjust the band — angle, background opacity, font size, position, image width,
   and the rules above and below.
4. Export as PDF, PNG, or JPEG at 300 DPI, or print directly.

Space under the image is left free so "สำเนาถูกต้อง", the signature, and the date can
be written by hand. A pre-printed block is available behind a toggle if you prefer.

## Notes on Thai usage

- Write the purpose across the image itself, not beside it, so it cannot be cropped away.
- Name the recipient organisation, and include the 13-digit registration number when
  the copy goes to a company — the narrower the stated purpose, the less the copy can
  be reused.
- Under ป.พ.พ. มาตรา 1143 a private limited company cannot hold its own shares, so a
  copy supporting a share transfer should name an individual transferee rather than
  say the shares return to the company.

## Local development

No build step and no dependencies. Open `index.html` in a browser, or serve the
directory:

```sh
python3 -m http.server 8777
```

## Licence

MIT
