# docs.stevedores.org

Routing layer for `docs.stevedores.org`. Aggregates per-repo documentation sites and serves them under path-based routing.

## Architecture

Each repository in `stevedores-org` has its own `docs-site/` directory with a self-contained React + Vite + Tailwind SPA. This repo aggregates them behind a single nginx reverse proxy:

| Path | Repo | Description |
|------|------|-------------|
| `/llama-rs/` | [llama.rs](https://github.com/stevedores-org/llama.rs) | Minimal LLM inference engine |
| `/oxidizedMLX/` | [oxidizedMLX](https://github.com/stevedores-org/oxidizedMLX) | Rust-first MLX tensor runtime |
| `/oxidizedRAG/` | [oxidizedRAG](https://github.com/stevedores-org/oxidizedRAG) | High-performance GraphRAG |
| `/oxidizedgraph/` | [oxidizedgraph](https://github.com/stevedores-org/oxidizedgraph) | Agent orchestration framework |

## Deployment

### Docker Compose (recommended)

```bash
docker compose up --build -d
```

This builds all four docs sites from source and serves them on port 80.

### Individual site development

Each site can be developed independently:

```bash
cd /path/to/repo/docs-site
bun install
bun run dev
```

## Stack

- **Proxy**: nginx:alpine
- **Docs sites**: React 19 + Vite 7 + Tailwind CSS v4 + Bun
- **Build**: Multi-stage Docker (oven/bun:1 -> nginx:alpine)
