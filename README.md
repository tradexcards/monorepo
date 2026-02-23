# TradeX Monorepo

Perpetual futures trading platform for TCGPlayer cards on Solana.

## Structure

| Directory | Repository | Description |
|-----------|------------|-------------|
| `program/` | [perp-program](https://github.com/tradexcards/perp-program) | Solana program (Rust) |
| `backend/` | [backend](https://github.com/tradexcards/backend) | API server & oracle keeper (Bun/TypeScript) |
| `frontend/` | [frontend](https://github.com/tradexcards/frontend) | Web UI (SvelteKit) |
| `mcp-server/` | [mcp](https://github.com/tradexcards/mcp) | MCP server for AI agents |
| `SKILL/` | [SKILL](https://github.com/tradexcards/SKILL) | Agent skill definitions |
| `APIs/` | [APIs](https://github.com/tradexcards/APIs) | TCGPlayer API response examples |

## Quick Start

```bash
# Clone with submodules
git clone --recursive git@github.com:tradexcards/monorepo.git
cd monorepo

# Or if already cloned without --recursive
git submodule update --init --recursive

# Copy environment config
cp .env.example .env
# Edit .env with your values

# Install dependencies
cd backend && bun install && cd ..
cd frontend && bun install && cd ..

# Run backend
cd backend && bun run dev

# Run frontend (separate terminal)
cd frontend && bun run dev
```

## Mainnet Deployment

- **Program**: `TRDXCHHWWZdQXxkGFJxek1KU2hn19687xztNBy99Ca1`
- **Authority**: `CARDC7GG52NdYwhSRBdAm46dV6X1qPUU9yyWSPSChXUE`

## License

MIT
