# Raza Petroleum ERP — GitHub version

The program is one web page (`index.html`) hosted free on **GitHub Pages**. Your data is one file, `data.json`, in a **private GitHub repository**. Every phone/PC that opens the page loads and saves that same file. **No Firebase, no other service.**

| File | What it is |
|---|---|
| `index.html`, `manifest.webmanifest`, `icon-*.png` | the program (no data inside) — goes in the **public** website repository |
| `config.js` | optional: your GitHub user name + data repository name, so devices don't ask for them |
| `data.json` | **your current offline data** (all sales, ledgers, customers, stock…) — goes in the **private** data repository |

**Login:** user name `admin` — password `admin123`. Change both right after the first sign-in: **Setup → Users & Password → Change user name / password**. You can also add more users (admin or staff) there.

---
## One-time setup (about 10 minutes)

**1. Private data repository**
github.com → **New repository** → name `raza-erp-data` (no spaces) → **Private** → Create. Then **Add file → Upload files** → upload `data.json` → **Commit**.

**2. Access token**
github.com → your photo → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**. Repository access: **Only select repositories → raza-erp-data**. Permissions: **Contents → Read and write**. Choose the longest expiry, generate, and copy the token (starts with `github_pat_`).

**3. Website repository**
New **public** repository, e.g. `raza-erp`. Upload `index.html`, `config.js`, `manifest.webmanifest`, `icon-192.png`, `icon-512.png`. (Optional first: edit `config.js` and type your GitHub user name and `raza-erp-data`.) Then **Settings → Pages → Deploy from a branch → main → / (root) → Save**. After a minute the app is live at `https://YOUR-USERNAME.github.io/raza-erp/`.

**4. First open on each device**
Open the address. The **Cloud storage** box appears → enter user name, data repository name and the token → **Save & Connect**. Your data loads, then sign in with `admin` / `admin123`. The device remembers the connection.

> Do **not** put `data.json` in the public website repository — a public repository can be read by anyone.

## Updating the data on GitHub from your offline file
* **From the app:** press 📥 (top right) → choose your offline `.html` file or a `.json` export → confirm. It is saved to GitHub within 2 seconds (pill shows **☁ Synced**).
* **By hand:** on github.com open `raza-erp-data` → click `data.json` → ✏️ → or **Add file → Upload files** with a new `data.json` (same name replaces it).
* If `data.json` is missing from the data repository, the app offers to create it from your offline file when you connect.

## Everyday use
* Every entry is saved to GitHub 1–2 seconds after you make it; the pill at the top shows **☁ Synced**.
* No internet? Keep working — changes stay on that device and upload automatically when the connection returns.
* Two devices at once: a screen with nothing unsaved refreshes itself every 30 seconds. If both change data at the same moment you are asked which copy to keep.
* On a phone use **Add to Home Screen** to get an app icon.
* **Database & Export** (Menu → System) downloads every table as Excel, CSV or JSON. Use ⬇️ (full backup) weekly as a second copy. GitHub also keeps every earlier version of `data.json` in the repository's commit history.

## Troubleshooting
* **“401 Bad credentials”** — the token is wrong, incomplete or expired. Make a new one and paste all of it.
* **“404 / cannot find repository”** — the owner is your GitHub *user name* (not email); the repository name has no spaces; the token must be given access to that repository.
* **Forgot the app password?** On the sign-in screen press **Forgot password?**, paste your GitHub token. The login is reset to `admin` / `admin123`; then change it in Setup.
