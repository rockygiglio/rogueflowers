# Rogue Flowers — Hugo Site

A Hugo static site for Rogue Flowers, organized per the Hugo best-practices reference.

## Structure

```
hugo-site/
├── archetypes/                  # `hugo new` content templates
├── assets/                      # Hugo Pipes-processed assets
│   └── scss/
│       ├── main.scss            # Entry — only @imports
│       ├── _variables.scss      # Design tokens
│       ├── _base.scss           # Reset, typography, .wrap, eyebrows
│       ├── components/          # _buttons, _nav
│       └── layouts/             # _hero, _sections, _footer
├── config/
│   ├── _default/                # Base config
│   │   ├── hugo.toml            # Site config, permalinks, markup
│   │   ├── params.toml          # Brand, contact, social, stats
│   │   └── menus.toml           # Main + footer menus
│   └── production/params.toml   # Prod-only overrides (analytics)
├── content/                     # Markdown
│   ├── _index.md                # Home
│   ├── services/_index.md
│   ├── events/_index.md
│   ├── restaurants/_index.md
│   ├── process/_index.md
│   └── contact/_index.md
├── data/                        # Lightweight database
│   ├── services.yaml
│   ├── restaurants.yaml
│   ├── faq.yaml
│   ├── process.yaml
│   └── testimonials.yaml
├── layouts/
│   ├── baseof.html              # Outer shell
│   ├── home.html                # Homepage (composes section partials)
│   ├── page.html                # Default single
│   ├── section.html             # Default list
│   ├── _partials/
│   │   ├── head.html            # Pipes SCSS, fonts, SEO
│   │   ├── header.html          # Nav (loops Site.Menus.main)
│   │   ├── footer.html          # Footer (loops Site.Menus.footer_studio)
│   │   ├── contact-info.html    # Reused address/email/phone block
│   │   └── sections/            # Homepage section partials
│   │       ├── hero.html
│   │       ├── marquee.html
│   │       ├── services.html    # Loops Site.Data.services
│   │       ├── whom.html
│   │       ├── process.html     # Loops Site.Data.process
│   │       ├── gallery.html
│   │       ├── testimonial.html # Reads Site.Data.testimonials
│   │       ├── restaurants.html # Loops Site.Data.restaurants
│   │       ├── faq.html         # Loops Site.Data.faq
│   │       └── contact.html
│   └── _shortcodes/
│       └── placeholder.html     # Reusable {{< placeholder variant="sage" label="..." >}}
└── static/
    ├── images/logo.png
    └── robots.txt
```

## Build

```bash
cd hugo-site
hugo server -D     # dev
hugo               # production build → ./public
```

## Editing common things

| Change | Where |
| --- | --- |
| Phone, email, address | `config/_default/params.toml` → `[contact]` |
| Brand colors | `config/_default/params.toml` → `[brand]` *and* `assets/scss/_variables.scss` |
| Add/edit a service | `data/services.yaml` |
| Add a restaurant account | `data/restaurants.yaml` |
| Add an FAQ | `data/faq.yaml` |
| Change main nav | `config/_default/menus.toml` |
| Section copy on home | the matching `layouts/_partials/sections/*.html` |
| Page copy | the page's markdown in `content/` |

## Notes

- All contact info pulls from `params.toml`. There are no hardcoded phone numbers.
- The site's striped image placeholders are CSS only — replace `<div class="ph">` blocks with real `<img>` tags (or page-bundle resources) as you get photography.
- Logo lives in `static/images/logo.png` (no Pipes processing needed for the favicon path).
