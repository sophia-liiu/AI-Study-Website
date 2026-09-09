# Notecard

Paste your notes in, get flashcards and a quiz out. A small single-page study tool — no build step, no backend, no account system.

## How it works

- Paste notes into the textarea and click **Generate flashcards**.
- The page calls the Anthropic API directly from your browser using your own API key, and asks Claude to turn your notes into flashcards and a multiple-choice quiz.
- Flip through flashcards, or switch to Quiz mode to test yourself with scoring.
- Your API key is saved only in your browser's local storage — it's never sent anywhere except Anthropic's API.

## Running it locally

It's a single HTML file. Just open `index.html` in a browser, or serve it locally:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

You'll need an Anthropic API key from [console.anthropic.com](https://console.anthropic.com/settings/keys). Paste it into "API key settings" on the page — it's saved for next time.

> Note: this calls the API directly from the browser, which is fine for a personal tool but means anyone with access to the page (and your key) could use it. Don't share a deployed link with your key pre-filled, and don't commit a key into the repo.

## Deploying to GitHub Pages

1. **Create a repository**
   - On GitHub, click **New repository**.
   - Name it anything, e.g. `notecard` (or `yourusername.github.io` if you want it at the root of your GitHub domain).
   - Make it public, don't initialize with a README (you already have one).

2. **Push your files**
   ```bash
   cd study-platform
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/notecard.git
   git push -u origin main
   ```
   (No git experience? You can also drag-and-drop `index.html` and `README.md` directly into the repo through GitHub's web UI using "Add file" → "Upload files".)

3. **Enable GitHub Pages**
   - In your repo, go to **Settings → Pages**.
   - Under "Build and deployment", set **Source** to `Deploy from a branch`.
   - Choose branch `main`, folder `/ (root)`, then **Save**.

4. **Visit your site**
   - After a minute or two, it'll be live at:
     `https://YOUR_USERNAME.github.io/notecard/`
   - (Or `https://YOUR_USERNAME.github.io/` if you named the repo `yourusername.github.io`.)

5. **Add it to your resume/portfolio**
   - Link to the live GitHub Pages URL, and link to the repo itself so people can see the code.

## Ideas to extend it later

- Save generated flashcard sets to `localStorage` so they persist across visits.
- Add spaced-repetition scheduling (e.g. show missed cards again sooner).
- Support uploading a PDF or `.txt` file instead of pasting text.
- Add a lightweight backend (Cloudflare Worker or similar) to proxy the API call, so you're not exposing a raw key in client-side JS for a wider audience.
