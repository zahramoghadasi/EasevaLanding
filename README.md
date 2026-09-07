# Easeva marketing site

Two pages:
- `index.html` — main landing page
- `waitlist.html` — waitlist signup page (linked from every "Join waitlist" button)

`apps-script-waitlist.gs` is not part of the website itself — it's the backend
script that goes into Google Sheets to receive waitlist submissions. See
"Backend setup" below.

## Publishing on GitHub Pages

1. Create a new repository on GitHub (or use an existing one for easeva.uk)
2. Add these files to the repo root — `index.html` and `waitlist.html` need
   to stay in the same folder together, since they link to each other by
   relative path (`waitlist.html`, `index.html`)
3. Push to GitHub
4. In the repo, go to **Settings > Pages**
5. Under "Build and deployment", set Source to **Deploy from a branch**,
   pick your main branch and `/ (root)`, then Save
6. GitHub gives you a URL like `https://yourusername.github.io/repo-name/`
   — if you're pointing your own domain (easeva.uk) at it, add a `CNAME`
   file (see below) and set up your domain's DNS to point at GitHub Pages

### Using your own domain (easeva.uk)

1. Create a file named `CNAME` (no extension) in the repo root containing
   just: `easeva.uk`
2. In your domain's DNS settings, point it at GitHub Pages following
   [GitHub's custom domain guide](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)
3. Back in repo Settings > Pages, enter `easeva.uk` under "Custom domain"

## Backend setup (waitlist submissions)

The waitlist form is already wired up to send data via `fetch()` — it just
needs a live endpoint to send it to. Full instructions are in the comments
at the top of `apps-script-waitlist.gs`. Short version:

1. Create a Google Sheet, add headers: `Timestamp | Name | Phone | Email | Device`
2. Extensions > Apps Script, paste in `apps-script-waitlist.gs`
3. Deploy > New deployment > Web app (Execute as: Me, Access: Anyone)
4. Copy the deployment URL (ends in `/exec`)
5. Open `waitlist.html`, find `WAITLIST_ENDPOINT` near the bottom of the
   file, and replace the placeholder with your URL

**Before this works, you must complete step 5** — right now
`WAITLIST_ENDPOINT` is a placeholder string, so submissions won't go
anywhere until it's replaced with a real deployment URL.

## To do before launch

- [ ] Replace the hero image placeholder in `index.html` with a real app screenshot
- [ ] Connect `WAITLIST_ENDPOINT` in `waitlist.html` to a live Apps Script deployment
- [ ] Confirm the "20 free spots" copy still matches your actual plan
- [ ] Decide on final FAQ pricing answer before it's public
