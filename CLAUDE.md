# TELLO AI — PROJECT LOCK

## THIS REPO IS THE ONLY TRUTH
- **Repo: `infomomtelo-sketch/tello`** — NOT `tello-ai` (that repo does not exist), not
  `tello-staff`, not `tello-runp8`. Ignore every other tello project and old code.
- Live site: https://infomomtelo-sketch.github.io/tello/ (GitHub Pages)
- First site Powered by Tello AI: **title-22.com**
- Worker: **https://tello-api.infomomtelo.workers.dev**

## STACK — DO NOT CHANGE MODEL NAMES
- Model: **`claude-sonnet-4-20250514`** ONLY. If you see `claude-3-5-sonnet-20241022`, it is WRONG.
- KV binding: `TELLO_MEMORY` → `tello-memory` namespace (memory works, `hasMemory: true`)
- R2 binding: `TELLO_FILES` → `tello-files` bucket. **Optional** — upload must keep working without it.
- Frontend: GitHub Pages, served from this repo.

## WHAT TELLO IS
Fresno RCFE Title 22 compliance AI by Eli, for his mom's 6-bed RCFE.
Features: floor plan upload (Claude Vision), KV memory, Title 22 §87307 checks, pricing $3500/bed.

Branding: "Use Tello AI for your Facility — Powered by Claude Sonnet 4 • Cloudflare Workers • Title 22 Engine"

## WHAT IS ACTUALLY IN THIS REPO
Frontend only. Three files:
- `index.html` — the whole app (hero, chat, upload, memory). Single file, no build, no dependencies.
- `manifest.json` — PWA manifest, linked from `index.html`.
- `README.md`

**The Worker source is NOT in this repo, and there is no `wrangler.toml` here.** Do not invent
either one. If a Worker change is needed, ask Eli where the Worker code lives.

## WORKER ENDPOINTS THE FRONTEND CALLS
| Call | Purpose |
| --- | --- |
| `POST /` with `{messages:[{role:'user',content}]}` | chat |
| `GET /connections` | returns `hasMemory`, `hasFiles`, `mcp` — the KV/R2 status pill |
| `POST /upload` with FormData `file` + `facility` | floor plan analysis (Claude Vision) |
| `POST /mcp/call` with `{tool, args}` | tools: `list_facilities`, `save_facility`, `recall_facility` |

## RULES
1. Only work in this repo. Never search or pull from other tello repos.
2. Always read `index.html` before editing it.
3. Never hallucinate old Tello code. If a file is missing, ask.
4. Keep the model at `claude-sonnet-4-20250514` and keep the Worker's CORS headers.
5. Never break the app when R2 is missing — surface the Worker's message, keep the page usable.
6. Render Worker replies with `textContent`, never `innerHTML` (they are untrusted output).
