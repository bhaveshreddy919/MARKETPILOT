# MarketPilot AI

Commerce intelligence dashboard helping small sellers and aspiring entrepreneurs evaluate products and discover what to sell using clearly labeled sample market signals.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 8080)
- `pnpm --filter @workspace/marketpilot-ai run dev` — run the MarketPilot AI dashboard
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- No database is used by the first version.
- `SERPAPI_API_KEY` is reserved for future server-side use; no API key is needed for the sample-data version.

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/marketpilot-ai` — MarketPilot AI React/Vite dashboard.
- `artifacts/api-server/src/routes/market.ts` — validated mock-analysis API routes.
- `artifacts/api-server/src/lib/market-data-provider.ts` — replaceable sample-data provider and calculated estimates.
- `lib/api-spec/openapi.yaml` — source of truth for the market API contract.

## Architecture decisions

- Market reports use a replaceable sample provider; live SerpApi integration is intentionally not connected in this version.
- Analysis is stateless and does not persist user inputs or reports.
- Sample metrics and calculated metrics are returned with explicit source labels.

## Product

- Analyze a product by name, location, and purchase cost; view an opportunity score, price range, gross-margin estimate, competition, demand momentum, customer signals, recommendation, comparisons, and a price trend.
- Discover ranked product opportunities by category, location, budget, target customer, and business goal.
- The dashboard clearly indicates that current market information is sample data and that SerpApi data is not connected.

## User preferences

- Keep the experience as a premium dark business-intelligence dashboard, not a conventional e-commerce storefront.
- Do not add authentication, accounts, saved history, payments, or database features to the first version.

## Gotchas

- When changing the API contract, regenerate hooks and Zod schemas with `pnpm --filter @workspace/api-spec run codegen`.
- Keep any future SerpApi credential on the server; never expose it to the frontend.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
