# JobHunt Platform

A CV and cover letter editor that runs entirely in your browser. One HTML file, no build step,
no server, no account, no tracking.

Write your CV inline on a real A4 page, tailor a copy per job application, track which applications
are out, and print to PDF. Everything stays on your machine.

**[Open the live version →](https://bragisnaer.github.io/jobhunt-platform/)**

Or download `index.html` and double-click it. It works from `file://` — no install, no internet
required after the first load (see [Third-party assets](#third-party-assets)).

---

## What it does

- **A4 CV editor** — click any text to edit it. Real page geometry, so what you see is what prints.
- **Three templates** — `editorial`, `editorial mirror` (sidebar flipped), and `linear`. Switch at any
  time; your content follows.
- **Cover letter** — matching document with an addressable sender block, recipient, subject, and
  sign-off. Seeds itself from your CV contact details on first use.
- **Applications tracker** — one bundle per job application, each owning its own CV, cover letter,
  headshot, and status. Fork a "Base" application to tailor a variant without touching the original.
  Custom statuses, colours, and ordering.
- **Headshot editor** — upload, crop to six shapes, pan, zoom, resize. Stored as image bytes in
  IndexedDB, not as a bloated base64 string in your saved data.
- **Sidebar sections** — show, hide, reorder, rename, and duplicate. Competencies, languages with
  proficiency bars, tools, positions of trust, interests, places of residence.
- **Seven colour schemes**, adjustable typography and spacing.
- **Print to PDF** via your browser's print dialog. Filenames follow
  `<Name>_<CV|Cover-Letter>_<Application>`.
- **Export / import JSON** — your data, in a file you own.
- **Optional folder sync** — bind the app to a local folder and it writes `cv-data.json` plus an
  `images/` directory alongside `index.html`. Put that folder in Dropbox or OneDrive and your CV
  follows you between machines. Chromium-only; see below.

## Keeping a copy of your data

Your data lives in your browser's `localStorage` and `IndexedDB`, scoped to whichever address you
opened the page from. Nothing is stored anywhere else, which means **you are responsible for backups**.

- **Back up** downloads a single JSON file containing every application, its CV, its cover letter, and
  its headshot. **Restore** reads that file back. This works in every browser and is the way to move
  your data between machines.
- **Clearing site data deletes your CV.** There is no server-side copy to recover from.
- **The hosted version and a downloaded copy are separate origins.** Data saved on
  `bragisnaer.github.io` does not appear in a local `index.html`, and vice versa. Export and import
  JSON to move between them.

### Limitation of the hosted version

On the hosted version, **JSON export and import is the only way to keep a local copy**. The
folder-sync mode is designed around a *folder package* — `index.html` sitting on your disk next to
its own `cv-data.json` and `images/` directory, the whole folder inside Dropbox or OneDrive. That
layout only exists if you download the file. If you want your CV to live as real files on your disk
rather than inside a browser profile, download `index.html` and run it from your own folder.

## Privacy

There is no backend, no analytics, no telemetry, no error reporting, and no account system. The app
makes no network requests of its own.

If you use folder sync, the app writes to a folder you explicitly pick. If that folder happens to be
inside a cloud-sync client, that client — not this app — uploads it.

### Third-party assets

Two things are fetched from other domains on load, both pinned to exact versions with
[subresource integrity](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity)
hashes so a compromised CDN cannot substitute different code:

- **React 18.3.1 and Babel standalone**, from unpkg. Babel compiles the JSX in the page at load time.
  That costs about 2 MB and a moment of startup, and it is the deliberate price of the whole app
  being one readable file you can fork and edit without a toolchain.
- **Inter Tight** from Google Fonts. This means Google sees your IP address when the page loads. If
  that bothers you, delete the three `<link>` tags near the top of `index.html` — the app falls back
  to a system font stack and everything still works.

To run fully offline, download the three scripts, drop them next to `index.html`, and point the
`<script src>` tags at the local copies.

## Browser support

| Feature | Chrome / Edge | Firefox | Safari |
|---|---|---|---|
| Editing, templates, print to PDF | ✅ | ✅ | ✅ |
| Headshot upload (IndexedDB) | ✅ | ✅ | ✅ |
| JSON export / import | ✅ | ✅ | ✅ |
| Folder sync (File System Access API) | ✅ | ❌ | ❌ |

On Firefox and Safari the sync UI is hidden and JSON export/import is the way to move data.

## Getting started

1. Open the [live version](https://bragisnaer.github.io/jobhunt-platform/) or download `index.html`.
2. The page loads with a fictional demo CV so you can see every section filled in. Click into it and
   start replacing text with your own.
3. Delete the sections you do not want from the sidebar panel.
4. *Back up* to JSON once you have something worth keeping.

## Development

There is no build. Open `index.html` in an editor, change it, reload the browser.

The file is organised in banner-commented blocks: seed data, storage schema and migrations, folder
sync, headshot editor, the CV document, the cover letter, the template registry, the toolbar, and the
applications tracker. Search for the `════` banners to navigate.

## Contributing

Issues and pull requests are welcome, but this is a personal project shared because it might be useful
to someone else. It is provided as-is and no support or response time is promised. If it does not do
what you need, forking it is entirely reasonable — that is what the licence is for.

## Licence

[MIT](LICENSE).
