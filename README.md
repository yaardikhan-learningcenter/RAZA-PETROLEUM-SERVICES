# Raza Petroleum ERP — cloud version

The program is one web page (`index.html`) hosted free on **GitHub Pages**. Your data lives in a **cloud database** that every phone and PC shares. Two choices — **Firebase is recommended** because the connection is set up **once** (in `config.js`) and each device only signs in with an email and password.

| File | What it is |
|---|---|
| `index.html`, `manifest.webmanifest`, `icon-*.png` | the program (no data inside) |
| `config.js` | your one-time connection settings (not secret) |
| `firestore.rules` | the security rules to paste into Firebase |
| `data.json` | **your current offline data** — uploaded to the cloud on first connect |

---
## A. Firebase (recommended) — about 15 minutes, free plan

1. Go to **console.firebase.google.com** → **Add project** (name e.g. `raza-petroleum-erp`; Google Analytics can be off).
2. **Build → Authentication → Get started → Sign-in method → Email/Password → Enable → Save.** Then open the **Users** tab → **Add user** → enter your email and a password. (Add one user per partner/manager who needs access.)
3. **Build → Firestore Database → Create database** → *Production mode* → choose a nearby location (e.g. `asia-south1`) → **Enable**.
4. In Firestore open the **Rules** tab, delete what is there, paste the content of `firestore.rules`, replace `YOUR-EMAIL@gmail.com` with the email(s) from step 2, and press **Publish**.
5. Click the gear ⚙ → **Project settings → General**. Copy the **Project ID** and the **Web API Key**.
6. Open `config.js` in a text editor, paste the Project ID and Web API key between the quotes, save.
7. On github.com create a **public** repository (e.g. `raza-erp`), **Add file → Upload files**: upload `index.html`, `config.js`, `manifest.webmanifest`, `icon-192.png`, `icon-512.png`. Then **Settings → Pages → Deploy from a branch → main → / (root) → Save**. After a minute the app is live at `https://YOUR-USERNAME.github.io/raza-erp/`.
8. Open that address. The **Cloud storage** box appears automatically → enter your Firebase email and password → **Sign in & Connect**.
9. The box says **“Cloud database is empty”** → press **Choose offline file…** and pick either your existing offline `.html` file or the `data.json` from this folder. Everything (sales, ledgers, customers, users…) is uploaded once.

**Every other device:** open the same address and sign in with the email and password — nothing else. The Project ID/key come from `config.js`, and the device stays signed in.

The Web API key in a public file is normal for Firebase — it only identifies your project. Your data is protected by the rules in step 4: nobody except the listed emails can read or write it.

## B. GitHub as the database (alternative)

Use this if you prefer not to use Firebase. Create a **private** repository for the data (e.g. `raza-erp-data`), upload `data.json` to it, create a fine-grained token (Contents: Read and write, only that repository) and enter it in the **GitHub repository** tab of the Cloud box on each device.

Common mistakes the app now warns about: the **owner** is your GitHub *user name* (not your email address); repository names cannot contain **spaces**; the data file must be named `data.json` (ending in `.json`); the token is long and starts with `github_pat_`. “401 Bad credentials” always means the token is wrong, incomplete or expired.

---
## Everyday use
* Every entry is saved to the cloud 1–2 seconds after you make it; the pill at the top shows **☁ Synced**.
* No internet? Keep working — changes are kept on that device and uploaded automatically when the connection returns.
* Two devices at once: a screen with nothing unsaved refreshes itself every 30 seconds. If both change data at the same moment you are asked which copy to keep.
* On a phone use **Add to Home Screen** to get an app icon. The ＋ button opens quick entry.
* **Database & Export** (Menu → System) downloads every table as Excel, CSV or JSON.
* **Setup → Users & Password** turns on the in-app sign-in screen (admin/staff).
* Move offline data in any time with 📥 (accepts the offline `.html` or a `.json` export).

## Safety
* Keep Firestore rules as given; never switch the database to “test mode”.
* Use ⬇️ (full backup) weekly as a second copy.
* **Forgot the app (Users) password?** On the sign-in screen press **Forgot password?** and enter your Firebase password (or GitHub token). The app sign-in is switched off so you can create a new admin under Setup → Users & Password.
