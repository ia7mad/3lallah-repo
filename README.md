# 3lallah Repo

A self-hosted, AltStore-compatible IPA source hosted on GitHub Pages.

**Source URL:** `https://3lallah.live/repo.json`

Works with Feather, AltStore, SideStore, and any IPA store that supports AltStore-style JSON sources.

---

## Repository Layout

```
3lallah-repo/
├── repo.json      # AltStore-compatible source manifest
├── index.html     # Landing page
├── ipa/           # IPA binaries (uploaded manually)
├── icons/         # App icon images
└── README.md      # This file
```

---

## How to Add a New App

1. Upload the `.ipa` file to the [`ipa/`](ipa/) folder (see the upload instructions below).
2. Upload the app's icon image (PNG, ideally 512×512) to the [`icons/`](icons/) folder.
3. Open [`repo.json`](repo.json) and append a new object to the `apps` array:

   ```json
   {
     "name": "App Name",
     "bundleIdentifier": "com.developer.appname",
     "developerName": "Developer Name",
     "subtitle": "Short tagline",
     "version": "1.0.0",
     "versionDate": "2026-05-16",
     "versionDescription": "What's new in this version.",
     "downloadURL": "https://3lallah.live/ipa/appname-1.0.0.ipa",
     "iconURL": "https://3lallah.live/icons/appname.png",
     "tintColor": "#00C6FF",
     "size": 12345678,
     "localizedDescription": "Full description of the app.",
     "minOSVersion": "14.0",
     "screenshotURLs": [],
     "permissions": []
   }
   ```

4. Commit and push to `main`. GitHub Pages will publish the updated `repo.json` within a minute.

### Field notes

- **`bundleIdentifier`** — must match the IPA's actual bundle ID (reverse-DNS style).
- **`size`** — IPA file size in **bytes** (right-click → Properties, or run `wc -c < file.ipa`).
- **`versionDate`** — ISO 8601 date, e.g. `2026-05-16`.
- **`downloadURL`** — must point to the public GitHub Pages URL of the IPA, not the raw GitHub URL.

---

## How to Upload an IPA

1. Drop the `.ipa` into the `ipa/` folder (locally or via the GitHub web upload).
2. Use a clean filename — lowercase, no spaces, include the version: `myapp-1.2.3.ipa`.
3. Commit and push.

> GitHub has a **100 MB per-file limit**. For larger IPAs use [Git LFS](https://git-lfs.com) or host the binary on a GitHub Release and link to that asset URL in `downloadURL`.

---

## How to Update an Existing App Version

1. Upload the new IPA to `ipa/` (use a new filename with the new version number — keep the old one if you want users to be able to downgrade).
2. In [`repo.json`](repo.json), find the app's entry and update:
   - `version` → new version number
   - `versionDate` → today's date
   - `versionDescription` → changelog for this release
   - `downloadURL` → URL of the new IPA
   - `size` → new file size in bytes
3. Commit and push. AltStore-style clients will detect the new version and show an update.

> Tip: bump the `version` string so it is **strictly greater** than the previous one (semver works fine: `1.0.0` → `1.0.1`).

---

## GitHub Pages

This repo is served by GitHub Pages from the `main` branch root. After the first push, enable Pages under **Settings → Pages → Source: Deploy from a branch → `main` / `/ (root)`**.
