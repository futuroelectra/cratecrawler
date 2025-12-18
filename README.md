# Crate Crawler Landing Page

A tiny static landing page for **Crate Crawler**, deployed on GitHub Pages and wired to an n8n workflow.

## Tech stack

- Single `index.html` file
- [Tailwind CSS](https://cdn.tailwindcss.com) via CDN (no build step)
- Vanilla JavaScript `fetch` call to an n8n webhook
- Deployable directly to GitHub Pages

## Editing the n8n webhook URL

1. Open `index.html`.
2. Find this line near the bottom:

   ```js
   const N8N_WEBHOOK_URL = 'https://YOUR_N8N_INSTANCE/webhook/your-workflow-id';
   ```

3. Replace the placeholder string with your actual n8n webhook URL.
4. Commit and push the change; the live site will use the new endpoint.

The payload sent to n8n is:

```json
{
  "email": "user@example.com",
  "discogsUrl": "https://www.discogs.com/..."
}
```

## Running locally

No tooling is required.

1. Clone the repository.
2. Open `index.html` directly in your browser (double-click it or drag it into a browser window).
3. The form will work as long as `N8N_WEBHOOK_URL` points to a reachable n8n instance.

## Enabling GitHub Pages

1. Push this repo to GitHub (see commands below).
2. In GitHub, go to **Settings → Pages**.
3. Under **Source**, choose:
   - **Deploy from a branch**
   - **Branch:** `main`
   - **Folder:** `/ (root)`
4. Click **Save**.
5. After a minute or two, GitHub will show the live URL, typically:

   ```text
   https://YOUR_GITHUB_USERNAME.github.io/REPO_NAME/
   ```

## Setting a custom domain (`www.cratecrawler.com`)

### 1. Configure GitHub Pages

1. In GitHub, go to **Settings → Pages**.
2. Under **Custom domain**, enter:

   ```text
   www.cratecrawler.com
   ```

3. Click **Save**.
4. GitHub will create a `CNAME` file in the repo automatically and provision HTTPS (may take several minutes).

### 2. Configure DNS in Namecheap

In your Namecheap dashboard for `cratecrawler.com`:

1. Go to **Domain List → Manage → Advanced DNS**.
2. Make sure you are using **Namecheap BasicDNS** or another provider where you can edit records.

Create/update these records:

- **CNAME record**  
  - **Host:** `www`  
  - **Value/Target:** `YOUR_GITHUB_USERNAME.github.io.`  
  - **TTL:** `30 min` or `Automatic`

- **URL Redirect record (optional but recommended)**  
  - **Type:** `URL Redirect Record`  
  - **Host:** `@`  
  - **Value:** `https://www.cratecrawler.com`  
  - **Redirect type:** `Permanent (301)`

DNS propagation can take up to an hour, but often completes faster. Once done, `https://www.cratecrawler.com` should show your GitHub Pages site over HTTPS.

## Git commands to create and push the repo

From the project folder containing `index.html`:

```bash
git init
git add index.html README.md
git commit -m "Initial Crate Crawler landing page"
git branch -M main
git remote add origin git@github.com:YOUR_GITHUB_USERNAME/cratecrawler-landing.git
git push -u origin main
```

Then follow the **Enabling GitHub Pages** section above to put it live.
# cratecrawler
# cratecrawler
