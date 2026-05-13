# Glitch Edge — docs site

Source for [docs.edge.glitchexecutor.com](https://docs.edge.glitchexecutor.com) (or
whatever subdomain we land on). Built with [Mintlify](https://mintlify.com).

## Structure

```
docs.json                  Mintlify config — theme, nav, OpenAPI source
favicon.png                32x32 favicon
logos/glitch-edge.svg      Brand mark
getting-started/           Onboarding pages
concepts/                  Strategy DSL, bankroll, settlement, audit
api/                       OpenAPI + MCP narrative pages
```

The **API reference** tab is auto-generated from
`https://edge.glitchexecutor.com/api/openapi.json` (the live OpenAPI spec the
running FastAPI service publishes). No hand-written API reference pages.

## Local dev

```bash
# Requires the Mintlify CLI
npx mint dev
# or
bunx mint dev
```

Then open http://localhost:3000.

## Deployment

Mintlify deploys this repo on every push (once connected in their dashboard):

- Project ID: `69f9a8b0543b139f956fb075`
- Connected branch: `main`

## Editing

- All content is MDX. Mintlify components (`<Card>`, `<Steps>`, `<AccordionGroup>`,
  `<CodeGroup>`, etc.) are documented at https://mintlify.com/docs.
- `docs.json` is the single source for nav. Add a page → add it to `navigation.tabs[*].groups[*].pages`.
- Brand color is `#0164ff`. Don't drift without updating the SPA + Astro site too.

## What lives elsewhere

- Marketing site → `glitch-edge-site` repo (Astro)
- Web app → `glitch-edge-app` repo (React)
- API → `glitch-edge-api` repo (FastAPI)
- The OpenAPI spec this site renders → published by the API automatically
