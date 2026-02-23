# TradeX Monorepo

Perpetual futures DEX for TCGPlayer cards on Solana.

## Structure

```
tradex-monorepo/
├── .env                 # Single config file (copy from .env.example)
├── keypair.json         # Admin keypair (git-ignored)
├── program/             # Solana program (Rust)
├── backend/             # API server & oracle keeper (Bun/Elysia)
├── frontend/            # Web UI (React/Bun)
├── mcp-server/          # MCP server for AI agents
├── SKILL/               # Agent skill definitions
└── APIs/                # TCGPlayer API response examples
```

## Submodules

Each directory is a git submodule with its own repo. When making changes:

1. Make changes in the submodule directory
2. Commit and push the submodule: `cd backend && git add -A && git commit -m "msg" && git push`
3. Update the monorepo reference: `cd .. && git add backend && git commit -m "Update backend submodule" && git push`

## Environment

Single `.env` at monorepo root. All submodules use `--env-file=../.env`.

Key variables:
- `PROGRAM_ID` - Solana program: `TRDXCHHWWZdQXxkGFJxek1KU2hn19687xztNBy99Ca1`
- `SOLANA_RPC_URL` - RPC endpoint (use Helius/QuickNode for mainnet)
- `ADMIN_PASSWORD` - Admin API password (16+ chars)
- `KEYPAIR_PATH` - Path to admin keypair (`./keypair.json`)

## Commands

Run from monorepo root:

```bash
bun install              # Install all deps
bun run dev              # Run backend + frontend in parallel
bun run dev:backend      # Backend only
bun run dev:frontend     # Frontend only
bun run build            # Build all packages
```

## Bun

Use Bun for everything. Don't use Node.js, npm, yarn, or pnpm.

- `bun <file>` not `node <file>`
- `bun install` not `npm install`
- `bun run <script>` not `npm run <script>`
- `bun test` not `jest`

Bun APIs:
- `Bun.serve()` for HTTP/WebSocket servers (not express)
- `Bun.file()` for file I/O (not fs.readFile)
- `Bun.$\`cmd\`` for shell commands (not execa)
- `bun:sqlite` for SQLite (not better-sqlite3)

## Backend

Elysia framework on Bun. Key files:
- `src/index.ts` - Entry point
- `src/routes/` - API endpoints
- `src/services/oracle/keeper.ts` - Oracle price updates & market creation
- `src/env.ts` - Environment config

The keeper service auto-initializes oracle state and creates markets from `initial-feeds.txt` on startup.

## Frontend

React with Bun's HTML imports. No Vite.
- `src/index.ts` - Bun.serve() entry
- `src/index.html` - HTML entry with script imports
- `src/lib/config.ts` - Reads `BUN_PUBLIC_*` env vars

## Program

Solana program in Rust (no Anchor). Key paths:
- `src/` - Program source
- `scripts/` - Deployment scripts (build.sh, deploy.sh, init-exchange.ts)
- `target/deploy/tradex_program.so` - Compiled binary

Deploy commands:
```bash
cd program
bun run build           # Build program
bun run deploy          # Deploy to network
bun run init-exchange   # Initialize exchange state
bun run status          # Check on-chain state
```

## On-Chain State

- Program: `TRDXCHHWWZdQXxkGFJxek1KU2hn19687xztNBy99Ca1`
- Authority: `CARDC7GG52NdYwhSRBdAm46dV6X1qPUU9yyWSPSChXUE`
- USDC Mint: `EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v` (mainnet)
