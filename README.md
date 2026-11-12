# Passport Photo Editor

Create, edit, and prepare passport, visa, and ID photos for printing — right in your browser. The project also includes an Electron desktop app for Windows, macOS, and Linux.

**Live demo:** https://iambhargavnath.github.io/pp-editor/

**Repository:** https://github.com/iambhargavnath/pp-editor

---

## Features

- **Country-specific photo sizes** — presets for India/UK, USA, Canada, Schengen, and China, plus custom sizing in the print workflow.
- **Crop and transform** — crop, rotate, flip, reset, or skip cropping.
- **Background tools** — remove the background with on-device AI segmentation and replace it with a preset or custom solid color.
- **Photo adjustments** — brightness, contrast, saturation, exposure, sharpness, and filter presets.
- **Virtual formal wear** — optional suit and blazer overlays.
- **Live Camera Studio** — capture photos with face-framing guidance, stability feedback, quality checks, and automatic/burst capture features.
- **Batch processing** — add multiple photos and choose the number of copies for each.
- **Print-ready layouts** — arrange photos on an A4 sheet and export as PDF or JPG.
- **Individual exports** — download an edited photo, or download multiple photos as a ZIP.
- **PWA support** — install the web app on supported browsers; a service worker caches app resources for offline use after the first successful load.
- **Desktop app** — package the project with Electron for Windows, macOS, and Linux.
- **Privacy-focused processing** — photo editing and AI inference run locally in the browser/desktop app; photos are not uploaded to an application server.

> **Important:** Photo-size presets and framing guidance are provided as editing aids, not a guarantee of acceptance by a passport, visa, or government authority. Requirements can change and may differ by application type. Always verify the current official photo specifications before submitting or printing.

## Live Demo

Open **[iambhargavnath.github.io/pp-editor](https://iambhargavnath.github.io/pp-editor/)** to use the web version.

## Getting Started

### Run locally in a browser

This is a static web app. You can serve the project directory with any local HTTP server.

For example, with Python:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

You can also use the VS Code **Live Server** extension.

> Use a local server rather than opening `index.html` directly. Service workers and some browser features require an HTTP(S) origin.

### Run the desktop app

**Requirements:** Node.js 20 or later and npm.

```bash
npm install
npm start
```

### Build desktop installers

```bash
# Build for the current platform
npm run dist

# Build for a specific platform
npm run dist:mac
npm run dist:win
npm run dist:linux

# Build for all supported platforms
npm run dist:all
```

Build output is written to the `dist/` directory.

## Deploy to GitHub Pages

This repository is intended to be published at:

`https://iambhargavnath.github.io/pp-editor/`

1. Create a GitHub repository named **`pp-editor`** under [iambhargavnath](https://github.com/iambhargavnath).
2. Extract the project files from this repository/archive.
3. Put the contents of the `passport-photo-generator-main/` folder in the **root** of the `pp-editor` repository. In particular, `index.html`, `css/`, `js/`, `assets/`, `manifest.json`, and `service-worker.js` should be at the repository root level.
4. Commit and push the files to the `main` branch.
5. In GitHub, open **Settings → Pages**.
6. Under **Build and deployment**, choose **Deploy from a branch**.
7. Select **`main`** and the **`/ (root)`** folder, then save.
8. Wait for the Pages deployment to finish. Your site will be available at:

   `https://iambhargavnath.github.io/pp-editor/`

The app uses relative asset paths, so it can be hosted from the `/pp-editor/` project subpath without changing the source paths.

### Optional: deploy with GitHub Actions

You can alternatively configure GitHub Pages to use a GitHub Actions workflow. For a simple static site, the branch-based deployment above is sufficient; the existing workflow in `.github/workflows/` is for building desktop installers, not publishing the website.

## Tech Stack

- HTML5, CSS3, and vanilla JavaScript
- Canvas API for photo rendering and print layouts
- [Cropper.js](https://github.com/fengyuanchen/cropperjs) for image cropping
- [jsPDF](https://github.com/parallax/jsPDF) for PDF export
- [JSZip](https://stuk.github.io/jszip/) for ZIP downloads
- MediaPipe Tasks Vision for optional on-device background segmentation and face landmark analysis
- Web Workers and OffscreenCanvas for image-quality analysis where supported
- Service Worker and Web App Manifest for PWA capabilities
- [Electron](https://www.electronjs.org/) and [electron-builder](https://www.electron.build/) for desktop builds

Some libraries are loaded from public CDNs. AI models and supporting runtime assets may also be fetched from external hosts when those optional features are first used. As a result, the initial load and some AI features require an internet connection; offline availability depends on which resources have already been cached.

## Privacy

- Uploaded photos are processed locally in the browser or desktop app.
- The application does not send user photos to an application backend.
- Optional AI features download their runtime/model assets from external providers; image analysis itself is performed locally on the device.
- Camera access is requested only when the Live Camera Studio is used.

For best privacy and security, use a trusted browser, keep it up to date, and review any third-party CDN dependencies before deploying a modified version.

## Project Structure

```text
pp-editor/
├── assets/                  # App icons and static assets
├── css/
│   ├── styles.css           # Main application styles
│   └── camera-studio.css    # Live Camera Studio styles
├── js/
│   ├── vendor/              # Bundled third-party libraries
│   ├── editor.js            # Main editing workflow
│   ├── cameraStudio.js      # Live camera capture and guidance
│   ├── backgroundRemoval.js # On-device background removal
│   ├── faceDetect.js        # Face detection and auto-crop support
│   ├── qualityWorker.js     # Image quality analysis worker
│   ├── canvasRenderer.js    # Canvas rendering utilities
│   ├── pdfGenerator.js      # PDF generation utilities
│   ├── photoUpload.js       # Photo upload utilities
│   └── i18n.js              # Language support
├── .github/
│   └── workflows/
│       └── build-desktop.yml # Cross-platform desktop build workflow
├── index.html
├── manifest.json
├── service-worker.js
├── main.js                  # Electron main process
├── preload.js
└── package.json
```

## Desktop Build Automation

The included GitHub Actions workflow builds desktop packages for macOS, Windows, and Linux when a version tag beginning with `v` is pushed. It can also be run manually from the Actions tab. Build artifacts are uploaded to the workflow run, and tagged builds can create a GitHub Release.

For example:

```bash
git tag v2.1.0
git push origin v2.1.0
```

## Contributing

Contributions, bug reports, and feature suggestions are welcome.

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/my-feature`.
3. Make and test your changes locally.
4. Commit your changes: `git commit -m "Add my feature"`.
5. Push your branch and open a Pull Request.

Please include clear steps to reproduce bugs and, where possible, screenshots of UI issues. Avoid including real passport/identity photos in public issues or pull requests.

## License

This project is distributed under the **MIT License**. See the [`LICENSE`](LICENSE) file for details.

---

## Author

**Bhargav Nath**  
GitHub: [@iambhargavnath](https://github.com/iambhargavnath)

**Copyright © 2026 Bhargav Nath.**
