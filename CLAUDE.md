# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Tales From The Friendly Arm Inn** is a comprehensive guide website for the EET (Enhanced Edition Trilogy), IWD1-EET, and IWD2-EET mods for Baldur's Gate. The site provides:

- Quest walkthroughs and guides
- Item/weapon/armor databases
- NPC information and recruitment guides
- Enemy strategies and boss guides
- Spell databases
- General gameplay guides

**Technology Stack:**
- Jekyll 4.3 (Static Site Generator)
- GitHub Pages (Hosting)
- Multi-language support (Japanese/English)
- JSON for structured data (items, NPCs, enemies, spells)
- Markdown for quest content

## Development Commands

### Local Development

```bash
# Install dependencies
bundle install

# Start local development server (http://localhost:4000)
bundle exec jekyll serve

# Start with live reload and incremental builds
bundle exec jekyll serve --livereload --incremental

# Build for production
JEKYLL_ENV=production bundle exec jekyll build
```

### Testing

```bash
# Check for broken links
bundle exec htmlproofer ./_site --disable-external

# Validate Jekyll configuration
bundle exec jekyll doctor
```

## Project Architecture

### Directory Structure

- `_config.yml` - Jekyll configuration, site settings, collections
- `_data/` - JSON data files for database content
  - `weapons.json`, `armor.json`, `items.json` - Equipment databases
  - `npcs.json` - NPC/companion data
  - `enemies.json` - Enemy and boss data
  - `spells.json` - Spell database
  - `navigation.json` - Site navigation structure
- `_layouts/` - Page templates
  - `default.html` - Base layout with header/footer
  - `home.html` - Homepage layout
  - `quest.html` - Quest page template
  - `database.html` - Database listing pages
- `_includes/` - Reusable components
  - `header.html`, `footer.html` - Site chrome
  - `item-card.html` - Reusable item display component
- `_quests/` - Quest content in Markdown
- `assets/` - Static assets
  - `css/style.css` - Main stylesheet with CSS variables
  - `js/main.js` - Client-side JavaScript
  - `images/` - Image assets
- `database/` - Database index pages (weapons, armor, items, npcs, enemies, spells)
- `quests/` - Quest listing pages
- `guides/` - General guide pages

### Data-Driven Content

Database pages use Jekyll's `site.data` to render JSON content dynamically. Each database page:
1. Loads data from `_data/*.json`
2. Renders items using `item-card.html` include
3. Provides filtering and search via JavaScript

### Multi-Language Support

Content uses language keys in JSON:
```json
{
  "name": {
    "ja": "日本語名",
    "en": "English Name"
  }
}
```

Pages use `page.lang` to display appropriate language version.

## Adding Content

### Adding a Quest

Create a new Markdown file in `_quests/`:

```markdown
---
layout: quest
title: "Quest Title"
mod: EET|IWD1-EET|IWD2-EET
type: メインクエスト|サイドクエスト
level: 3-5
lang: ja
rewards:
  - "経験値: 1000XP"
  - "報酬金: 500ゴールド"
---

Quest content in Markdown...
```

### Adding Database Items

Add entries to appropriate JSON file in `_data/`:

**Weapons** (`_data/weapons.json`):
```json
{
  "id": "unique_id",
  "name": {"ja": "名前", "en": "Name"},
  "type": "longsword",
  "enchantment": 2,
  "damage": "1d8+2",
  "special": {"ja": "特殊効果", "en": "Special effect"},
  "location": {"ja": "入手場所", "en": "Location"},
  "usable_by": ["fighter", "paladin"],
  "image": "/assets/images/items/item.png"
}
```

**NPCs** (`_data/npcs.json`):
```json
{
  "id": "npc_id",
  "name": "NPC Name",
  "race": "Human",
  "class": "Fighter",
  "alignment": "Lawful Good",
  "description": {"ja": "説明", "en": "Description"},
  "stats": {"str": 18, "dex": 15, "con": 16, "int": 10, "wis": 12, "cha": 14},
  "location": {"ja": "場所", "en": "Location"},
  "recruitment": {"ja": "仲間にする方法", "en": "How to recruit"}
}
```

### Styling Guidelines

The site uses CSS custom properties (variables) defined in `assets/css/style.css`:
- `--primary-color`: Main theme color (brown)
- `--secondary-color`: Accent color (gold)
- `--background-color`: Page background (beige)
- Follow the medieval/fantasy aesthetic
- Ensure responsive design for mobile devices

## Deployment

The site deploys automatically via GitHub Actions when pushing to `main` branch.

**GitHub Pages Setup:**
1. Repository Settings > Pages
2. Source: "GitHub Actions"
3. Workflow file: `.github/workflows/jekyll.yml`

**Manual deployment steps (if needed):**
1. Build: `JEKYLL_ENV=production bundle exec jekyll build`
2. Deploy: Contents of `_site/` directory

## Design Philosophy

- Fantasy/medieval theme inspired by Baldur's Gate aesthetics
- Focus on readability and information density
- Mobile-responsive design
- Search and filter functionality for databases
- Structured JSON data for maintainability and reusability
