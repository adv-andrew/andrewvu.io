# My Hugo Blog

A beautiful blog built with Hugo and the PaperMod theme.

## Local Development

1. Start the development server:
   ```bash
   hugo server
   ```

2. View your blog at: `http://localhost:1313`

## Deploying to GitHub Pages with Custom Domain

### 1. Create GitHub Repository
1. Create a new repository on GitHub named `your-username.github.io`
2. Push your Hugo blog code to this repository

### 2. Set up GitHub Actions for Automatic Deployment
Create `.github/workflows/hugo.yml`:

```yaml
name: Deploy Hugo site to Pages

on:
  push:
    branches: ["main"]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

defaults:
  run:
    shell: bash

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          extended: true

      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v4

      - name: Build with Hugo
        env:
          HUGO_ENVIRONMENT: production
          HUGO_ENV: production
        run: |
          hugo \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/"

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deploy.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deploy
        uses: actions/deploy-pages@v4
```

### 3. Configure Custom Domain

1. **In your domain registrar (Namecheap, etc.):**
   - Add a CNAME record pointing your domain to `your-username.github.io`
   - For example: `www.yourdomain.com` → `your-username.github.io`

2. **In your GitHub repository:**
   - Go to Settings → Pages
   - Under "Custom domain", enter your domain name
   - Check "Enforce HTTPS"
   - GitHub will automatically create a CNAME file

3. **Update your Hugo configuration:**
   - Change `baseURL` in `hugo.yaml` to your custom domain

## Domain Setup Examples

### For GitHub Pages:
- CNAME record: `www.yourdomain.com` → `your-username.github.io`
- A record: `yourdomain.com` → `185.199.108.153` (GitHub Pages IP)

### DNS Propagation
- Can take 24-48 hours for global recognition
- Use `dig yourdomain.com` to verify DNS configuration

## Alternative Hosting Options

- **Netlify**: Easy custom domain setup with automatic SSL
- **Vercel**: Great performance with global CDN
- **Cloudflare Pages**: Fast with built-in optimization

## Troubleshooting

- Check DNS propagation: Use online DNS checker tools
- Verify CNAME file exists in your repository
- Ensure GitHub Pages is enabled in repository settings
- Contact your domain registrar or GitHub Support if needed 