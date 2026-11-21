# Quizykoo Learning — Master Brand Hub

## Site identity
- **Name**: Quizykoo Learning
- **Purpose**: Master brand hub linking all three book imprints
- **Live artifact**: https://claude.ai/artifact/QEWKsqGADfbaEmsfAe66G4 (Version 3)
- **Contact email**: hello@quizykoo.com

## File structure
```
index.html    ← single self-contained HTML page (logo embedded as base64 data URI)
```

No external images — the Quizykoo logo is embedded as a `data:image/png;base64,...`
data URI inside the HTML. If you need to swap the logo, re-generate the base64:

```bash
python3 -c "
import base64, sys
with open('Logo.png','rb') as f:
    print(base64.b64encode(f.read()).decode())
" > logo_b64.txt
```
Then find `data:image/png;base64,` in index.html and replace the base64 string.

To strip a white background before encoding (recommended for the dark footer):
```python
from PIL import Image
img = Image.open('Logo.png').convert('RGBA').resize((300,300))
data = img.load()
for y in range(img.height):
    for x in range(img.width):
        r,g,b,a = data[x,y]
        if r>230 and g>230 and b>230:
            data[x,y] = (r,g,b,0)
img.save('logo_transparent.png', optimize=True)
```

## Imprints linked
| Imprint | Books | Artifact URL |
|---------|-------|--------------|
| Life Skills Series | 20 Kindle eBooks | https://claude.ai/artifact/Lf11R3fiL2rMZgWc2bvM5Q |
| MythoKoo | 16 picture books | https://claude.ai/artifact/Rite3izNjGmm1q8YKLvvgK |
| WonderKoo | 55 picture books | https://claude.ai/artifact/DpVkotznafTUWyKuVFWp2R |

## Page sections (top → bottom)
1. **Nav** — sticky; Quizykoo logo + "Learning" wordmark; links to Our Books / About / Contact
2. **Hero** — tagline, stats (91 books, 3 imprints, Ages 4–12)
3. **Our Book Imprints** — 3 brand cards (Life Skills teal, MythoKoo dark-gold, WonderKoo navy-yellow)
4. **Testimonials** — 6 cards (2 per imprint), colour-badged
5. **About** — paragraph copy about Quizykoo Learning's mission
6. **Contact** — single email chip: hello@quizykoo.com
7. **Footer** — Quizykoo logo + "Learning" wordmark; imprint + page links; © 2026

## Design tokens
```css
--bg:       #FAFAF8   /* page background */
--bg2:      #F0EFEB   /* section / pill background */
--fg:       #1C2340   /* primary text */
--fg-mid:   #4B5468
--fg-muted: #6B7280
--accent:   #E07B2F   /* Quizykoo orange */
--radius:   18px
```

Imprint accent colours:
| Imprint | Header bg | Accent |
|---------|-----------|--------|
| Life Skills | `#1D8A99` teal | teal |
| MythoKoo | `#140722` indigo | `#c9a84c` gold |
| WonderKoo | `#192341` navy | `#f5c842` yellow |

Fonts: **Poppins** (headings, logo, stats) + **Inter** (body, nav, descriptions)  
Both loaded from Google Fonts.

## To update and publish via Claude Code
```
# Open in Claude Code, then in Claude:
# 1. Edit index.html as needed
# 2. Tell Claude: "Publish this to https://claude.ai/artifact/QEWKsqGADfbaEmsfAe66G4"
```

## Common edits
- **Change stats**: search `stat-num` in index.html — three `<span class="stat-num">` values
- **Update imprint card copy / pills**: find `<!-- Life Skills -->`, `<!-- MythoKoo -->`, `<!-- WonderKoo -->` comments
- **Add / edit testimonials**: find `<!-- TESTIMONIALS -->` comment; each card is a `.testi-card` div
- **Change email**: search `hello@quizykoo.com` (appears in contact section and footer links)
- **Update imprint artifact links**: the `card-btn` href values in each brand card

## Footer
© 2026 Quizykoo Learning · All rights reserved
Email: hello@quizykoo.com
