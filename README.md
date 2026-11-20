# my-direction-app (Direction Finder)

A Grade 8 student direction and strengths finder: pick interests, take a 5-question quiz built from those interests, see your top 3 directions, then chat with an AI mentor.

## Files

- `index.html` is the whole app (React, Tailwind and lucide icons loaded from CDNs).
- `api/chat.js` is the serverless function that talks to the Anthropic API.
- `lib/directions.json` is the directions dataset the function gives the AI.
- `vercel.json` adds basic security headers.

## Security

- The API key is read from the `ANTHROPIC_API_KEY` environment variable on the server only. It is not in the page, the repo or the browser.
- The function checks the request shape, caps message length and count, caps the reply size, and allows 20 requests per visitor per 10 minutes. That limit is best effort, because serverless instances do not share memory.
- Set a monthly spend limit for the key in the Anthropic Console. That is the real protection against misuse.
- `.env` is git-ignored. If a key is ever pasted into a commit, delete the key in the Console and create a new one.

## Push to GitHub

```
git init
git add .
git commit -m "Direction Finder"
git branch -M main
git remote add origin https://github.com/<your-username>/direction-finder.git
git push -u origin main
```

## Deploy on Vercel

1. Go to vercel.com, choose Add New, then Project, and import the GitHub repo.
2. Framework Preset: Other. Leave the build settings empty.
3. Open Environment Variables and add `ANTHROPIC_API_KEY` (create it at console.anthropic.com). Optionally add `ANTHROPIC_MODEL`.
4. Click Deploy, then open the Vercel URL.

If you add the key after the first deploy, redeploy once so the function picks it up.

## Without a key

The quiz and results still work. The mentor chat needs the key: without it, or if the API is unreachable, it shows a clear message instead of guessing.

---
made by AC Milan
