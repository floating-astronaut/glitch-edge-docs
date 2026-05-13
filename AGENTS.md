# Documentation project instructions

> For Mintlify product knowledge (components, configuration, writing standards),
> install the Mintlify skill: `npx skills add https://mintlify.com/docs`

## About this project

- This is the Mintlify-powered documentation site for **Glitch Edge**, the AI-automated
  sports betting + prediction markets platform at https://edge.glitchexecutor.com.
- Pages are MDX files with YAML frontmatter.
- Configuration lives in `docs.json`. Brand color is `#0164ff` — do not drift without
  updating the SPA + Astro marketing site at the same time.
- Run `mint dev` to preview locally; `mint broken-links` to validate references.
- Deploys via Mintlify's git integration on every push to `main`.

## Companion repos

| Repo | What | Touch from here? |
|---|---|---|
| `glitch-edge-api` | FastAPI backend that publishes `/api/openapi.json` | No — only consume the OpenAPI URL |
| `glitch-edge-app` | React SPA at `/app/` | No |
| `glitch-edge-site` | Astro marketing at `/` + `/pricing` | No — marketing copy belongs there, not here |
| `glitch-edge-docs` | **This repo** | Yes |

The **API reference** tab in `docs.json` is auto-generated from
`https://edge.glitchexecutor.com/api/openapi.json` (the live spec the running
FastAPI service publishes). Never hand-write API reference pages — change the
backend, push, and the docs site rebuilds on next Mintlify deploy.

## Terminology (use these spellings)

- **Strategy** — the user-authored rule document (not "bot", not "model")
- **Bet** — a single placement (paper or live). Bets on Polymarket are called **orders**.
- **Worker** — the server-side ticker that evaluates strategies. Not "engine", not "AI".
- **Settle watcher** — separate scheduled job that reconciles finished bets.
- **Cap** — `bankroll_cap` is rolling 24h; `stake_cap` is per-bet.
- **Token** — personal API key (`gle_<8>.<32>`). Not "secret", not "credential".
- **Cloudbet API key** — the user's external sportsbook credential. Always say
  "Cloudbet API key" in full to avoid confusion with our own token.
- **Paper / live** — never "demo" or "dummy". The worker distinguishes by a
  boolean column called `paper`; mirror that in copy.

## Style preferences

- Active voice, second person ("you paste your Cloudbet API key, the worker places…")
- Sentence-case headings (not Title Case)
- One idea per sentence — break long ones
- **Bold** for UI elements (`Click **Resume** on the strategy card`)
- `Code formatting` for file names, commands, paths, env vars, and route paths
- Numbers: spell out one through nine in prose; use digits for 10+ and all stats

## Content boundaries

- **Never** promise guaranteed returns, +EV picks, or "winning bots".
- **Never** imply Glitch Edge custodies funds. Cloudbet holds money; we automate.
- **Never** list Cloudbet-banned countries as supported. The TAM is everywhere
  except: Australia, Austria, Belgium, China, Macau, HK, Curaçao, Cuba, France,
  Germany, Iran, Lithuania, Malta, Myanmar, Netherlands, North Korea, Singapore,
  Syria, Spain, UK, US, parts of Ukraine. Always defer geo questions to Cloudbet's
  current ban list — don't enumerate it inline (changes occasionally).
- **OK** to discuss bankroll math, Kelly criterion, settlement logic, and how
  the worker decides whether to place a bet. That's the product story.

## Image + asset conventions

- Logos in `logos/`. Favicons in repo root (`favicon.png`).
- Don't drop raw `.png` files into the repo root other than `favicon.png` —
  put screenshots in `images/` with descriptive filenames.

## Routes that exist for AI to verify against

If you find yourself documenting a feature, check it exists. The canonical sources:

| Reference | URL |
|---|---|
| Live OpenAPI spec | https://edge.glitchexecutor.com/api/openapi.json |
| Swagger UI | https://edge.glitchexecutor.com/api/docs |
| Health check | https://edge.glitchexecutor.com/api/healthz |

If a feature appears in the OpenAPI spec it's real. If not, mark it as
roadmap in the docs (like `api/mcp.mdx` does) — do not invent shape.
