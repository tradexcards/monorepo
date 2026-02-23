# TradeX Monorepo

Perpetual futures trading platform for TCGPlayer cards on Solana.

## Structure

| Directory     | Repository                                                  | Description                                 |
| ------------- | ----------------------------------------------------------- | ------------------------------------------- |
| `program/`    | [perp-program](https://github.com/tradexcards/perp-program) | Solana program (Rust)                       |
| `backend/`    | [backend](https://github.com/tradexcards/backend)           | API server & oracle keeper (Bun/TypeScript) |
| `frontend/`   | [frontend](https://github.com/tradexcards/frontend)         | Web UI (React/Bun)                          |
| `mcp-server/` | [mcp](https://github.com/tradexcards/mcp)                   | MCP server for AI agents                    |
| `SKILL/`      | [SKILL](https://github.com/tradexcards/SKILL)               | Agent skill definitions                     |
| `APIs/`       | [APIs](https://github.com/tradexcards/APIs)                 | TCGPlayer API response examples             |

## Quick Start

```bash
# Clone with submodules
git clone --recursive git@github.com:tradexcards/monorepo.git
cd monorepo

# Or if already cloned without --recursive
git submodule update --init --recursive

# Copy environment config and edit with your values
cp .env.example .env

# Install all dependencies
bun install

# Run backend + frontend in parallel
bun run dev
```

## Environment

All configuration is in a single `.env` file at the monorepo root. Copy `.env.example` to `.env` and fill in your values.

Key variables:
- `PROGRAM_ID` - Solana program address
- `SOLANA_RPC_URL` - RPC endpoint (use private RPC for mainnet)
- `ADMIN_PASSWORD` - Admin API password (16+ chars for mainnet)
- `KEYPAIR_PATH` - Path to admin keypair for oracle/keeper

## Scripts

| Command | Description |
|---------|-------------|
| `bun install` | Install dependencies for all packages |
| `bun run dev` | Run backend + frontend in parallel |
| `bun run dev:backend` | Run backend only |
| `bun run dev:frontend` | Run frontend only |
| `bun run build` | Build all packages |
| `bun run start` | Start backend + frontend (production) |

## Mainnet Deployment

- **Program**: `TRDXCHHWWZdQXxkGFJxek1KU2hn19687xztNBy99Ca1`
- **Authority**: `CARDC7GG52NdYwhSRBdAm46dV6X1qPUU9yyWSPSChXUE`

## License

MIT
