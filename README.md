# Mindful Design Documentation

Official documentation for Mindful Design WordPress plugins.

## Quick Start

### Prerequisites

- Python 3.8+
- pip

### Installation

```bash
# Install dependencies
pip install -r requirements.txt

# Or install directly
pip install mkdocs-material
```

### Local Development

```bash
# Start local server
mkdocs serve

# Open http://127.0.0.1:8000 in your browser
```

### Deploy to GitHub Pages

```bash
# Build and deploy
mkdocs gh-deploy
```

## Structure

```
mindfuldesign-docs/
├── mkdocs.yml              # Configuration
├── docs/
│   ├── index.md            # Homepage
│   └── mindfulmedia/       # MindfulMedia plugin docs
│       ├── index.md
│       ├── getting-started.md
│       ├── shortcodes.md
│       ├── features/
│       ├── settings/
│       ├── page-builders/
│       └── developer/
└── requirements.txt
```

## Adding Screenshots

Place screenshots in `docs/assets/images/mindfulmedia/` and reference them:

```markdown
![Description](../assets/images/mindfulmedia/filename.png)
```

## Adding New Plugins

1. Create a folder: `docs/newplugin/`
2. Add an `index.md` overview
3. Add to `mkdocs.yml` navigation
4. Create feature/settings/developer docs as needed

## Custom Domain Setup

1. Enable GitHub Pages in repo settings
2. Set source to `gh-pages` branch
3. Add custom domain: `docs.mindfuldesign.me`
4. Create CNAME record in DNS pointing to `mindfuladmin.github.io`

## License

Documentation content is proprietary to Mindful Design.
