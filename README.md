# Power Meter Packer

Single-page tool: reads a Granite Excel file plus a ZIP of field photos (TB/ODB fibre boxes with power meters), pairs the 1310/1550 nm photos per port, and builds a PowerPoint (one slide per port) and an Excel table of readings and missing pictures.

## Files
- `index.html` - the whole app (HTML, CSS, JS in one file). Libraries load from CDNs (JSZip, PptxGenJS, SheetJS).

## Important: how it reads photos
This version calls `window.claude.use('sample')` and `window.claude.use('downloads')`. These exist only when the page runs as a Claude artifact. On GitHub Pages or any other host they are missing, so:
- the Granite file, ZIP loading, pairing, review table and missing-pictures list do not need them,
- reading the photos and saving the downloads do.

To run it from GitHub you need to replace two things:
1. Photo reading: send each batch of images to a vision model API with your own key (see `S.sample.json(...)` in `runBatches`).
2. Downloads: replace `S.dl.save({filename,data})` with a normal browser download (an `<a download>` link to a Blob URL).

## Publish on GitHub Pages
1. Create a repository and add `index.html` and this README.
2. Settings > Pages > Deploy from branch > `main` / root.
3. Open `https://<user>.github.io/<repo>/`.

Do not put an API key in a public page. Each user should paste their own key into the page, or use a small backend.
