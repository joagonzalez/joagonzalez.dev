# joagonzalez.dev

Personal portfolio site for [Joaquin Gonzalez](https://joagonzalez.dev).

Plain HTML/CSS/JS — no build step, no framework.

## Structure

```
joagonzalez.dev/
├── src/
│   ├── index.html
│   ├── style.css
│   └── main.js
├── Dockerfile
├── nginx.conf
└── .github/
    └── workflows/
        └── deploy.yml
```

## Local development

No build step required. Open `src/index.html` directly in a browser, or serve it with any static server:

```bash
npx serve src/
```

Or via Docker:

```bash
docker build -t joagonzalez.dev . && docker run -p 8080:80 joagonzalez.dev
```

Then open http://localhost:8080.

## Deployment

### GitHub Pages (production)

The site is deployed automatically to GitHub Pages on every push to `main` via the workflow at `.github/workflows/deploy.yml`.

**One-time setup:**

1. Go to the repository **Settings → Pages**
2. Set source to **GitHub Actions**
3. Add your custom domain under **Settings → Pages → Custom domain** (e.g. `joagonzalez.dev`)
4. Add the following DNS records with your domain registrar:

| Type | Name | Value |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `joagonzalez.github.io` |

5. Enable **Enforce HTTPS** once the domain is verified.

After that, every push to `main` deploys automatically.

### Docker (self-hosted / VPS)

```bash
docker build -t joagonzalez.dev .
docker run -d -p 80:80 --name joagonzalez.dev joagonzalez.dev
```
