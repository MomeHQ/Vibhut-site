# Deploy vibhut.com — FESTIVE version

End-to-end: ~30 min active work + DNS propagation overnight.

## What this is

The **festive** version of the Vibhut splash. Lively, warm, celebration energy:

- Drifting marigold petals (8 petals, slow continuous fall, rotating)
- Twinkling gold sparkle fireflies (8 fixed-position, fade in/out)
- Lantern garland strung across hero (7 small lanterns)
- TWO Mitras flanking the logo (mirror), bouncy entry, gentle bobble
- Bouncy logo pendant entry (overshoots and settles)
- Gold shimmer effect on "Traditions" headline (animated background gradient)
- Mitra portrait wobbles gently side to side
- 3 sparkle stars rotating around Mitra portrait
- Bouncier hover lifts on all cards (translateY + scale)
- More pronounced flame flicker on footer diyas
- Rotating rangoli mandala behind heritage section (16-fold symmetry)
- Pulsing logo glow in nav

Design philosophy: festival energy, warmth, joy. Things move with character.

## What's in this folder

```
vibhut-festive/
├── index.html              ← Splash page (festive)
├── privacy/
│   └── index.html          ← Privacy policy
├── terms/
│   └── index.html          ← Terms of service
├── assets/
│   ├── logo.png
│   └── mitra.png
├── CNAME
└── DEPLOY.md
```

## Deploy steps

### 1. Create GitHub repo (5 min)
- https://github.com/MomeHQ → New Repository
- Name: `vibhut-site`
- Public, no README/license/gitignore

### 2. Push code (5 min)
```powershell
# Drop all files into C:\projects\vibhut-site preserving structure
cd C:\projects\vibhut-site
git init
git branch -M main
git add .
git commit -m "Initial Vibhut splash (festive)"
git remote add origin https://github.com/MomeHQ/vibhut-site.git
git push -u origin main
```

### 3. Enable GitHub Pages (2 min)
- github.com/MomeHQ/vibhut-site → Settings → Pages
- Source: Deploy from a branch
- Branch: `main` / `(root)`
- Save

Wait 30 seconds, visit `https://momehq.github.io/vibhut-site/` to confirm it works.

### 4. Custom domain (3 min)
- Settings → Pages → Custom domain → `vibhut.com` → Save

### 5. GoDaddy DNS (10 min)

| Type | Name | Value | TTL |
|------|------|-------|-----|
| A | @ | 185.199.108.153 | 1 hour |
| A | @ | 185.199.109.153 | 1 hour |
| A | @ | 185.199.110.153 | 1 hour |
| A | @ | 185.199.111.153 | 1 hour |
| CNAME | www | momehq.github.io | 1 hour |

Delete existing parking-page records first.

### 6. Wait for DNS (1-24h)
Check at https://dnschecker.org

### 7. Enable HTTPS
- Settings → Pages → wait green ✅
- Check "Enforce HTTPS"

### 8. Fill in placeholders
In `privacy/index.html` and `terms/index.html`:
- `[INSERT DATE]` → `May 12, 2026`
- `[Your street address]` → MomeHQ's registered address

```powershell
git add . && git commit -m "Fill in placeholders" && git push
```

## Performance notes (festive version)
- Petals + sparkles run on CSS animations (GPU-accelerated, very low cost)
- All animations respect `prefers-reduced-motion` — older devices and accessibility-conscious users see static page
- Total DOM weight similar to cinematic (~400 elements)
- Should perform identically on iPhone 8+ / Android 7+
