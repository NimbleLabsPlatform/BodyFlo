# NimbleLabs — Deployment Guide
## GitHub Pages + Namecheap DNS

---

## Your File Structure

```
nimblelabs/
├── index.html         → https://nimblelabs.io/
├── privacy/
│   └── index.html     → https://nimblelabs.io/privacy
├── terms/
│   └── index.html     → https://nimblelabs.io/terms
└── CNAME              → tells GitHub Pages your custom domain
```

---

## Step 1 — Create a GitHub Repository

1. Go to [github.com](https://github.com) and sign in (or create a free account).
2. Click **"New repository"** (the green button or the `+` icon).
3. Name it exactly: **`nimblelabs.io`**
   - (or any name you prefer — the CNAME file handles the domain)
4. Set it to **Public**.
5. Leave everything else as default and click **"Create repository"**.

---

## Step 2 — Upload Your Files

### Option A: Drag & Drop (easiest)
1. Open your new repository on GitHub.
2. Click **"uploading an existing file"** or drag files into the page.
3. Upload all files **maintaining the folder structure**:
   - `index.html`
   - `privacy/index.html`
   - `terms/index.html`
   - `CNAME`
4. Click **"Commit changes"**.

### Option B: Git command line
```bash
cd path/to/nimblelabs/
git init
git add .
git commit -m "Initial site deploy"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/nimblelabs.io.git
git push -u origin main
```

---

## Step 3 — Enable GitHub Pages

1. In your repository, go to **Settings** (top tab).
2. In the left sidebar, click **"Pages"**.
3. Under **"Source"**, select **"Deploy from a branch"**.
4. Set Branch to **`main`** and folder to **`/ (root)`**.
5. Click **Save**.

GitHub will show a green banner: *"Your site is live at https://YOUR_USERNAME.github.io/nimblelabs.io"*

> The CNAME file you uploaded will also appear under **"Custom domain"** automatically. If not, type `nimblelabs.io` there and click Save.

6. Check **"Enforce HTTPS"** once it becomes available (may take a few minutes after DNS is configured).

---

## Step 4 — Configure Namecheap DNS

1. Log in to [namecheap.com](https://namecheap.com).
2. Go to **Domain List** → click **"Manage"** next to `nimblelabs.io`.
3. Click the **"Advanced DNS"** tab.
4. **Delete** any existing A records or CNAME records for `@` and `www`.
5. Add the following records:

| Type  | Host | Value                   | TTL        |
|-------|------|-------------------------|------------|
| A     | @    | `185.199.108.153`        | Automatic  |
| A     | @    | `185.199.109.153`        | Automatic  |
| A     | @    | `185.199.110.153`        | Automatic  |
| A     | @    | `185.199.111.153`        | Automatic  |
| CNAME | www  | `YOUR_USERNAME.github.io` | Automatic  |

> Replace `YOUR_USERNAME` with your actual GitHub username.

6. Click **Save All Changes**.

---

## Step 5 — Wait for DNS Propagation

DNS changes typically propagate within **15 minutes to 2 hours** (occasionally up to 48 hours in rare cases).

You can check propagation status at: https://dnschecker.org/#A/nimblelabs.io

Once propagated:
- `https://nimblelabs.io` → Home page ✅
- `https://nimblelabs.io/privacy` → Privacy Policy ✅
- `https://nimblelabs.io/terms` → Terms of Service ✅

---

## Troubleshooting

**Site shows "404 - There isn't a GitHub Pages site here"**
→ Wait a few more minutes for GitHub to build. Check Settings → Pages to confirm it's enabled.

**Custom domain shows an error**
→ Double-check the CNAME file contains only `nimblelabs.io` with no extra spaces. Verify DNS records match the table above exactly.

**HTTPS not working**
→ Wait up to 24 hours after DNS propagates. Then go to Settings → Pages and click "Enforce HTTPS."

**www.nimblelabs.io doesn't redirect**
→ Ensure you added the CNAME record for `www` pointing to `YOUR_USERNAME.github.io`.

---

## Updating Your Site Later

Simply edit the HTML files and push/upload them to GitHub. GitHub Pages automatically redeploys within ~1 minute.
