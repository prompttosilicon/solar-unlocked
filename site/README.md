# Solar Unlocked website

This folder contains the dependency-free Solar Unlocked project website and browser-based firmware installer. It is intended for GitHub Pages and introduces the project to non-developers before guiding them through hardware selection, installation, and setup.

## Local review

Web Serial requires a secure context. `localhost` is allowed, so serve this folder instead of opening `index.html` directly:

```powershell
cd github\site
python -m http.server 8000
```

Then open `http://localhost:8000` in desktop Chrome or Edge. You can review the page without connecting hardware. Clicking the installer button opens the serial-device picker.

## Files

- `index.html` — project homepage and installer
- `styles.css` — page styles
- `manifest.json` — ESP Web Tools manifest; flashes the merged factory image at address `0x0`
- `firmware/*-factory.bin` — complete first-install image
- `firmware/*-ota.bin` — application-only image for future OTA workflows
- `firmware/SHA256SUMS.txt` — release checksums

## GitHub Pages URL

If GitHub Pages publishes this folder as its artifact, the site will be available at the project root:

`https://prompttosilicon.github.io/solar-unlocked/`

If Pages is instead configured to publish the repository root directly, this folder will be available at `/site/`. A deployment workflow that uploads `github/site` is recommended so visitors receive the homepage at the project root.

Before publishing another version, update the binary filenames, `manifest.json`, the release details in `index.html`, and `SHA256SUMS.txt` together.

## Important behavior

The web installer is intended for a first-time factory install. The current merged image includes the bootloader, partition table, initial OTA metadata, and application. A factory install erases device flash and therefore removes NVS settings. It does not erase a removable microSD card.
