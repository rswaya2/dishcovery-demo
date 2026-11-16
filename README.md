# Dishcovery: hosted demo

Dish-first restaurant search for New York. A diner types a craving and gets matching
dishes from 207 menu records across ten restaurants. Code handles exact dishes and
ingredients; a small model (Claude Haiku 5.5) is called only to turn a vague craving
into search terms, and code then ranks, filters and cites the real records.

## What is in this folder

- `index.html`: the whole prototype (data, interface and code steps) in one file.
- `api/ask.js`: a small server function. It holds the Anthropic API key so visitors
  can use the AI step without one. It accepts only a craving and a model tier, adds the
  fixed system prompt itself, caps each connection at 30 searches per 10 minutes, and
  returns the model's search plan. It cannot be used as a general chat endpoint.

Opened directly from disk, `index.html` still works: code searches run live and the
AI step replays the model's real recorded outputs from 13 Nov 2026.

## Deploy on Vercel (free Hobby plan, about 15 minutes)

1. Anthropic Console: create a new API key for this demo only, and set a low monthly
   spend limit on the account (a few dollars is plenty; a Haiku search costs about $0.0002).
2. GitHub: create a new repository (public or private) and upload this folder's
   contents so that `index.html` and the `api` folder sit at the top level.
3. Vercel: sign up free with the GitHub account, choose Add New, then Project, and
   import the repository. Leave the framework setting as Other and the build settings empty.
4. Before deploying, open Environment Variables and add
   `ANTHROPIC_API_KEY` = your key. Then press Deploy.
   Optional, to limit live AI to people you give the link to: also add
   `DEMO_ACCESS_CODE` = a code you choose (letters and numbers, for example `dish2026nov`).
   Then share the link as `https://<project-name>.vercel.app/?code=dish2026nov`.
   Without the code, visitors still see the page, code search and the recorded replay,
   but cannot trigger live model calls.
5. Open the production link (`https://<project-name>.vercel.app`, plus `?code=...` if you set one), type a craving that
   is not on the recorded list (for example "warm noodle soup for a rainy day") and
   press Ask Dishcovery. The blue box should say "Live call via the hosted demo".
6. Share the production link only. Preview links (with extra words in the address)
   may ask visitors to log in to Vercel.

If the blue box says "Fallback", open the project in Vercel, go to Logs, and check the
error. The usual causes are a missing or mistyped key (redeploy after fixing it) or a
model name the account cannot use.

After grading, delete the key in the Anthropic Console to switch the AI step off.
The page keeps working with the recorded replay.

## Limits

The review paraphrases and linked photos come from third-party sources and have not
been cleared for publication. Every result shows its source and check date; menus change.
