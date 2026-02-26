# CLAUDE.md — joagonzalez.dev

## Project Overview

Personal portfolio website for Joaquin Gonzalez. Static single-page site with a terminal/CLI aesthetic theme.

## Tech Stack

- **Frontend:** Vanilla HTML5, CSS3, JavaScript (zero dependencies, no frameworks)
- **Server:** Nginx (Alpine) via Docker
- **Deployment:** Docker container serving static files on port 80

## Project Structure

```
├── src/                  # All source files served by Nginx
│   ├── index.html        # Single-page HTML (sections: hero, about, projects, contact)
│   ├── style.css         # Full stylesheet (dark terminal theme, responsive)
│   └── main.js           # Typing animation + scroll-based nav highlighting
├── prompts/              # AI context files (CV, profile) — not served
├── Dockerfile            # Alpine Nginx image, copies src/ to /usr/share/nginx/html/
├── nginx.conf            # Gzip, 1-year cache for assets, SPA fallback routing
└── .dockerignore
```

## Running Locally

```bash
# Option 1: Docker
docker build -t joagonzalez-site .
docker run -p 8080:80 joagonzalez-site

# Option 2: Any static file server
python -m http.server 8000 -d src/
```

## Design System

- **Theme:** Dark terminal aesthetic (background `#0d0d0d`, green `#3ddc84`, blue accent `#5555ff`)
- **Fonts:** System UI for body, `Courier New` monospace for terminal elements
- **Layout:** Max-width 740px, responsive grids via `auto-fit` + `minmax()`
- **Breakpoint:** 600px for mobile

## Key Patterns

- No build step — edit `src/` files directly
- No npm, no package.json, no bundler
- IntersectionObserver for active nav link tracking
- Typing animation cycles through CLI-style phrases
- Nginx config has gzip and aggressive caching for production

## Development Guidelines

- Keep zero-dependency philosophy — avoid adding frameworks or build tools
- All site content lives in `src/index.html` (single file, section-based)
- Styles are in one file (`src/style.css`) — no CSS preprocessor
- JS is minimal and vanilla (`src/main.js`) — no transpilation needed
- The `prompts/` directory contains CV/profile markdown for AI context, not part of the served site
- Test changes by opening `src/index.html` directly in a browser or using a local server

## Deployment (Planned)

- **Target:** VPS Kubernetes cluster
- **Kubeconfig:** `~/.kube/config_vps` (or similar name in that directory)
- **CI/CD:** GitHub Actions pipeline (not yet configured)
- **Flow:** Push to repo → GitHub Actions builds Docker image → deploys to K8s cluster
- **TODO:** Create GitHub Actions workflow, K8s manifests (Deployment, Service, Ingress), and configure secrets for kubeconfig access
