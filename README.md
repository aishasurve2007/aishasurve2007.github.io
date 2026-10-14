# Aisha Surve · Portfolio

Live site: https://aishasurve2007.github.io

## Files
- `index.html` — the whole website (HTML + CSS + JS, Three.js from a CDN). No build step.
- `Aisha_Surve_CV.pdf` — the CV (also embedded in the page for the Download CV button).
- `chat-backend/` — optional FastAPI server that gives the "Ask my portfolio" chat full AI answers.

## Edit content
Open `index.html` and change the `EDIT THIS PART` block at the top of the script:
`CONFIG`, `PROJECTS`, `MORE`, `EXPERIENCE`, `SKILLS`, `ABOUT`.

## 1. Put the site live (GitHub Pages)
1. Create a public repo named `aishasurve2007.github.io`.
2. Upload `index.html` and `Aisha_Surve_CV.pdf` to the root of the repo.
3. Settings → Pages → Source: Deploy from a branch → `main` / `(root)` → Save.
4. Wait 1–2 minutes, then open https://aishasurve2007.github.io

Without the backend, the chat still works: it shows the most relevant notes it retrieved.

## 2. Turn on full AI answers (optional, Render free tier)
1. Push this repo (or just `chat-backend/`) to GitHub.
2. render.com → New → Web Service → pick the repo.
   - Root directory: `chat-backend`
   - Build command: `pip install -r requirements.txt`
   - Start command: `uvicorn main:app --host 0.0.0.0 --port $PORT`
3. Environment variables:
   - `OPENAI_API_KEY` = your key
   - `ALLOWED_ORIGINS` = `https://aishasurve2007.github.io`
   - `OPENAI_MODEL` = optional, defaults to `gpt-4o-mini`
4. Deploy, then check `https://YOUR-SERVICE.onrender.com/health`.
5. In `index.html`, set `CHAT_ENDPOINT: "https://YOUR-SERVICE.onrender.com/ask"` and push.

Notes: the free Render tier sleeps after inactivity, so the first question can take ~30 s
(the site falls back to retrieved notes if it times out or fails). The server rate-limits
each visitor to 10 questions a minute to protect your API key. Never put the key in `index.html`.

## Run the backend locally
```bash
cd chat-backend
pip install -r requirements.txt
export OPENAI_API_KEY=sk-...
export ALLOWED_ORIGINS=http://localhost:5500
uvicorn main:app --reload
```
Serve the site with VS Code Live Server (port 5500) and set `CHAT_ENDPOINT` to `http://localhost:8000/ask`.
