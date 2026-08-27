# Enable GitHub Pages for this folder

1. Push the `docs/` folder to your repository root (same level as the Arduino sketch, or only `docs/` content as needed).
2. Repo → **Settings** → **Pages**.
3. **Source**: Deploy from a branch.
4. **Branch**: `main` (or `master`), folder **`/docs`**.
5. Save. After 1–2 minutes open:

   `https://<user>.github.io/<repo>/`

6. Install only works over **HTTPS** (or localhost) in **Chrome / Edge**.

## Checklist before public install

- [ ] `firmware/esp32c3/*.bin (C3 only)` present (see `firmware/HOW_TO_ADD_BINS.md`)
- [ ] Version string in `manifest.json` updated
- [ ] Footer link in `index.html` points to your real GitHub repo
- [ ] Tested on a real ESP32-C3 with data USB cable
