# Filaxy PDF Converter — Landing

Marketing site for **Filaxy PDF Converter**, a free, open-source macOS app that
converts any PDF into a faithful, editable Word document — and then verifies its
own work, line by line.

**Live:** https://pdfconverter.filaxy.net
**App repo:** https://github.com/othmarodev/filaxy-pdf-converter

## Stack

Plain HTML/CSS/JS, fully self-contained (CSS and JS embedded in `index.html`),
no build step. Deployed to Cloudflare Pages.

## Local preview

```bash
python3 -m http.server 8770
# open http://localhost:8770
```

Assets use absolute paths (`/assets/...`), so serve over HTTP — opening
`index.html` via `file://` will break them.

## License

[MIT](LICENSE)
