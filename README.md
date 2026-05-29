# docs.stevedores.org

Routing layer for `docs.stevedores.org`. Aggregates per-repo documentation sites and serves them under path-based routing.

## Architecture

Each repository in `stevedores-org` has its own `docs-site/` directory with a self-contained React + Vite + Tailwind SPA. This repo aggregates them behind a single nginx reverse proxy:

### ML & Inference

| Path | Repo | Description |
|------|------|-------------|
| `/llama-rs/` | [llama.rs](https://github.com/stevedores-org/llama.rs) | Minimal LLM inference engine |
| `/llama-cpp/` | [llama.cpp](https://github.com/stevedores-org/llama.cpp) | LLM inference in C/C++ |
| `/oxidizedMLX/` | [oxidizedMLX](https://github.com/stevedores-org/oxidizedMLX) | Rust-first MLX tensor runtime |
| `/mlx/` | [mlx](https://github.com/stevedores-org/mlx) | Apple MLX framework |

### Data & RAG

| Path | Repo | Description |
|------|------|-------------|
| `/oxidizedRAG/` | [oxidizedRAG](https://github.com/stevedores-org/oxidizedRAG) | High-performance GraphRAG |
| `/data-fabric/` | [data-fabric](https://github.com/stevedores-org/data-fabric) | Data fabric layer |

### Agents & Orchestration

| Path | Repo | Description |
|------|------|-------------|
| `/oxidizedgraph/` | [oxidizedgraph](https://github.com/stevedores-org/oxidizedgraph) | Agent orchestration framework |
| `/ai-agent-agent-guides/` | [ai-agent-agent-guides](https://github.com/stevedores-org/ai-agent-agent-guides) | AI agent guides |
| `/ai-agent-ci/` | [ai-agent-ci](https://github.com/stevedores-org/ai-agent-ci) | AI agent CI tooling |
| `/ai-agent-docs/` | [ai-agent-docs](https://github.com/stevedores-org/ai-agent-docs) | AI agent documentation |

### Developer Tools

| Path | Repo | Description |
|------|------|-------------|
| `/aivcs/` | [aivcs](https://github.com/stevedores-org/aivcs) | AI-powered version control |
| `/local-ci/` | [local-ci](https://github.com/stevedores-org/local-ci) | Local CI runner |
| `/gitoxide/` | [gitoxide](https://github.com/stevedores-org/gitoxide) | Rust git implementation |
| `/libgit2/` | [libgit2](https://github.com/stevedores-org/libgit2) | Git library |
| `/nix-cache/` | [nix-cache](https://github.com/stevedores-org/nix-cache) | Nix binary cache |

### Infrastructure

| Path | Repo | Description |
|------|------|-------------|
| `/crossplane-heaven/` | [crossplane-heaven](https://github.com/stevedores-org/crossplane-heaven) | Crossplane infrastructure |
| `/DevProd-AI/` | [DevProd-AI](https://github.com/stevedores-org/DevProd-AI) | Developer productivity AI |
| `/knittingCrab/` | [knittingCrab](https://github.com/stevedores-org/knittingCrab) | KnittingCrab tooling |
| `/stevedores-org/` | [stevedores.org](https://github.com/stevedores-org/stevedores.org) | Main website |

## Deployment

### Docker Compose (recommended)

```bash
docker compose up --build -d
```

This builds all docs sites from source and serves them on port 80.

### Production (builds from GitHub)

```bash
docker compose -f docker-compose.prod.yml up --build -d
```

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
