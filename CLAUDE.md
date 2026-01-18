# CLAUDE.md - AI Assistant Guide for Dominion of Light Project Site

This document provides comprehensive guidance for AI assistants working on the Dominion of Light (DOL) project documentation site.

## Project Overview

**Dominion of Light** is a procedurally generated, free-to-play roleplaying game of magic and mystery. This repository (`dol-project-site`) is a Jekyll-based documentation site hosted on GitHub Pages that serves as the central hub for game design documentation, features, and development roadmap.

**Key Information:**
- **Project Type:** Jekyll Static Site Generator + Documentation
- **Theme:** just-the-docs (0.5.0) - pinned version
- **Hosting:** GitHub Pages
- **Live URL:** https://bcolemutech.github.io/dol-project-site
- **Repository:** https://github.com/bcolemutech/dol-project-site
- **Purpose:** Document game features, mechanics, and development roadmap

## Repository Structure

```
dol-project-site/
├── _config.yml              # Jekyll site configuration
├── index.md                 # Home page with mission, roadmap, resources
├── Gemfile                  # Ruby dependencies
├── Gemfile.lock             # Locked dependency versions
│
├── Features/                # Game feature documentation
│   └── Maps.md              # Map generation system documentation
│
├── _data/                   # Jekyll data files
│   └── docs.yml             # Documentation navigation structure
│
├── .github/workflows/       # CI/CD automation
│   ├── pages.yml            # Deploy to GitHub Pages
│   └── pr.yml               # Markdown linting on PRs
│
└── .vscode/                 # VSCode settings
    └── settings.json        # Custom dictionary, YAML schemas
```

## Technology Stack

### Core Technologies
- **Jekyll 4.3:** Static site generator
- **Ruby 3.1:** Runtime environment (in CI/CD)
- **just-the-docs 0.5.0:** Documentation theme (pinned)
- **GitHub Pages:** Hosting platform

### Game Development Technologies (Referenced)
- **.NET & C#:** Game development framework
- **Unity:** Game engine for PC version
- **Spectre.Console:** Console UI framework
- **Rider IDE:** Development environment
- **Azgaar's Fantasy Map Generator:** Third-party map creation tool

### Development Tools
- **write-good:** Markdown linting in PRs
- **VSCode:** Recommended editor with custom settings

## Development Workflows

### Local Development Setup

To work with this site locally:

```bash
# Install dependencies
bundle install

# Serve the site locally (with auto-reload)
bundle exec jekyll serve

# Build the site
bundle exec jekyll build
```

### Branch Strategy

- **main:** Production branch, auto-deploys to GitHub Pages
- **Feature branches:** Use `claude/` prefix for AI assistant work
- Always create PRs for review before merging to main

### CI/CD Pipelines

#### GitHub Pages Deployment (`.github/workflows/pages.yml`)
- **Trigger:** Push to `main` branch or manual dispatch
- **Process:**
  1. Checkout code
  2. Setup Ruby 3.1 with bundler caching
  3. Configure GitHub Pages
  4. Build Jekyll site with production environment
  5. Upload artifact
  6. Deploy to GitHub Pages
- **Environment:** `JEKYLL_ENV=production`

#### Markdown Linting (`.github/workflows/pr.yml`)
- **Trigger:** Pull requests
- **Process:**
  1. Run write-good linter on markdown files
  2. Post linting feedback as PR comment
- **Tool:** tomwhross/write-good-action@v1.6

## Documentation Conventions

### File Organization

#### Documentation Pages
All documentation pages should:
- Be placed in appropriate directories (`Features/`, root for main pages)
- Use `.md` extension (Markdown)
- Include YAML front matter
- Follow naming conventions (PascalCase for feature names)

#### Front Matter Structure

**Home Page Pattern:**
```yaml
---
title: Home
layout: home
nav_order: 1
---
```

**Feature Page Pattern:**
```yaml
---
title: [Feature Name]
layout: default
nav_order: [Number]
---
```

### Navigation Management

Navigation is controlled through:
1. **Front matter:** `nav_order` field determines page order
2. **_data/docs.yml:** Defines documentation structure and URLs

**docs.yml Structure:**
```yaml
docs_list_title: DOL Features
docs:
  - title: [Feature Name]
    url: Features/[FeatureName].html
```

### Content Writing Guidelines

1. **Structure:**
   - Use clear heading hierarchy (H1 → H6)
   - Start with H1 for page title (automatically from front matter)
   - Use H2 for major sections, H3 for subsections

2. **Lists and Tables:**
   - Use markdown tables for feature comparisons and roadmaps
   - Use ordered lists for sequential processes/algorithms
   - Use unordered lists for feature sets and properties
   - See `Features/Maps.md:24-98` for complex list examples

3. **Links:**
   - Always use full URLs for external resources
   - Internal links use relative paths
   - Link to third-party tools and documentation

4. **Code and Technical Content:**
   - Use inline code for property names, file names
   - Use numbered lists for algorithms (see population determination algorithm in Maps.md)
   - Include specific numerical values and formulas where relevant

5. **Emojis:**
   - Used sparingly in roadmap features for visual categorization
   - 🖥️ for Console App features
   - 🎮 for Unity App features
   - 💰 for Greenlight/Release features

## Key Files and Their Purposes

### `_config.yml`
Jekyll site configuration with:
- Site title and description
- Theme specification
- Base URL for GitHub Pages
- Auxiliary links

**Important:** Don't modify theme name or URL without testing deployment.

### `index.md`
Home page containing:
- Project introduction and mission statement
- Third-party resources and links
- Development roadmap with version tracking
- Feature tables organized by development phase

**Update when:**
- Mission or goals change
- New third-party tools are adopted
- Roadmap phases are updated
- Features are completed (add version numbers)

### `Features/Maps.md`
Detailed documentation of map generation system including:
- Integration with Azgaar's tool
- Map object structure
- Location generation algorithms
- Population calculations
- City classification rules
- Special location rules

**Update when:**
- Map generation algorithms change
- New location types are added
- Population formulas are adjusted
- City of Light special buildings change

### `_data/docs.yml`
Documentation navigation index.

**Update when:**
- New feature documentation pages are added
- Page URLs change
- Documentation structure is reorganized

### `.vscode/settings.json`
Editor configuration with:
- Custom spell-check dictionary (Azgaar's, Greenlight)
- YAML schema mappings for Jekyll validation

**Update when:**
- New domain-specific terms need spell-check exceptions
- Additional schema validation is needed

## How to Add New Feature Documentation

Follow these steps to add a new feature page:

1. **Create the markdown file:**
   ```bash
   # Create file in Features directory
   touch Features/[FeatureName].md
   ```

2. **Add front matter:**
   ```yaml
   ---
   title: [Feature Name]
   layout: default
   nav_order: [Next Number]
   ---
   ```

3. **Write content following conventions:**
   - Start with H1 (title from front matter)
   - Use H2 for major sections
   - Include algorithms, rules, and specifications
   - Add relevant links and references

4. **Update `_data/docs.yml`:**
   ```yaml
   - title: [Feature Name]
     url: Features/[FeatureName].html
   ```

5. **Test locally:**
   ```bash
   bundle exec jekyll serve
   # Visit http://localhost:4000
   ```

6. **Create PR with changes:**
   - Markdown linter will run automatically
   - Address any linting feedback
   - Merge to main to deploy

## Important Rules and Conventions

### Content Philosophy

1. **Design Documentation, Not Code:**
   - This is a design specification repository
   - Document game mechanics, rules, and algorithms
   - Include specific formulas and calculations
   - No actual game code lives here

2. **Specificity Matters:**
   - Include exact numbers (population formulas, size thresholds)
   - Document all rules and exceptions
   - Specify algorithms step-by-step
   - See Maps.md for examples of detailed specifications

3. **Consistency:**
   - Follow established patterns from existing pages
   - Use similar structure for similar content types
   - Maintain consistent terminology
   - Reference the same third-party tools consistently

### Version Control

1. **Commits:**
   - Clear, descriptive commit messages
   - Reference features or sections being updated
   - Examples from history:
     - "Details for population adjustments"
     - "Add location factoring notes for burgs"
     - "Update Maps.md"

2. **Pull Requests:**
   - Automatic markdown linting runs
   - Review linting feedback in PR comments
   - Address issues before merging

### Dependencies and Versions

1. **Pinned Versions:**
   - just-the-docs is pinned to 0.5.0
   - Don't upgrade without testing
   - Document version changes in commit messages

2. **Ruby Version:**
   - CI/CD uses Ruby 3.1
   - Match this in local development if possible

### Testing Before Deployment

Always test changes locally:
```bash
bundle exec jekyll serve --watch
```

Check for:
- Proper rendering of markdown
- Working navigation links
- Correct front matter
- Table formatting
- List formatting
- External links

## Game Design Context

Understanding the game helps create better documentation:

### Core Game Principles

1. **Unlimited Gameplay:**
   - Procedural generation ensures no two games are the same
   - World evolves with AI-based factions
   - Dynamic quest generation

2. **Character Progression:**
   - Skill-based system (not point-based)
   - Skills improve based on usage/playstyle

3. **World Scale:**
   - Massive open world (improbable to explore entirely)
   - Persistent world that changes on revisit
   - Evolving ecosystems and factions

4. **Development Phases:**
   - **Console App:** Backend mechanics and algorithm testing
   - **Unity PC Game:** Full game with UI
   - **Steam Greenlight:** Public testing and refinement

### The City of Light

Special location in the game world:
- Always the largest capitol city
- Size increased 3x during map generation
- Contains unique special buildings (listed in Maps.md:84-93)
- Central to the game's story

### Azgaar's Integration

The game uses Azgaar's Fantasy Map Generator for world creation:
- Players create maps externally
- Export as JSON files
- Import into game for procedural enhancement
- See Maps.md for detailed processing rules

## Common Tasks for AI Assistants

### Updating the Roadmap

Location: `index.md:47-76`

To mark a feature as completed:
```markdown
| 🖥️ Console App            | 1.0.0   |
| 🖥️ Import game map        | 1.1.0   |
```

### Adding Game Mechanics Documentation

1. Create new file in `Features/`
2. Follow Maps.md structure as template
3. Include algorithms with numbered steps
4. Specify all rules and exceptions
5. Add cross-references to related features

### Updating Third-Party Resources

Location: `index.md:30-39`

Add new tools following the pattern:
```markdown
- [Tool Name](https://tool-url.com/)
```

### Fixing Markdown Linting Issues

Common write-good issues:
- Passive voice
- Weasel words
- "There is/are" constructions
- Repeated words
- Wordy phrases

Address in subsequent commit or PR update.

## Questions and Clarifications

When uncertain about:
- **Game mechanics:** Reference existing feature docs or ask for clarification
- **Structure changes:** Follow established patterns
- **New sections:** Model after Maps.md structure
- **Deployment issues:** Check GitHub Actions logs

## Final Notes

This is a **living documentation site** for a game in active design. The documentation should:
- Be clear and specific
- Include all relevant details
- Follow established patterns
- Maintain consistency
- Support the game development process

When in doubt, prioritize clarity and detail over brevity. This documentation serves as the specification for implementing game features.
