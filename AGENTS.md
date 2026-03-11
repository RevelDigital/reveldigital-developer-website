# AGENTS.md - Revel Digital Developer Website

## Project Overview

This is the Revel Digital developer documentation website. It provides API references and development guides for integrating with the Revel Digital digital signage platform.

## Tech Stack

- **Static Site Generator**: MkDocs with the Material for MkDocs theme
- **Source docs directory**: `mkdocs/` (configured via `docs_dir` in `mkdocs.yml`)
- **Build output directory**: `docs/` (configured via `site_dir` in `mkdocs.yml`, served via GitHub Pages)
- **Configuration**: `mkdocs.yml`

## Documentation Pages

| Page | Source File | Description |
|------|------------|-------------|
| Home | `mkdocs/index.md` | Introduction and navigation to all sections |
| REST API | `mkdocs/rest-api.md` | Programmatic access to Revel Digital account data |
| GraphQL API | `mkdocs/graphql.md` | Strongly-typed GraphQL interface for queries and mutations |
| Gadgets | `mkdocs/gadgets.md` | Dynamic template components (weather, calendar, etc.) |
| Webapps | `mkdocs/webapps.md` | Self-contained web apps using Angular, React, or Vue |
| Player API for Windows | `mkdocs/windows.md` | Runtime scripting for Windows-based signage |
| Player API for Android | `mkdocs/android.md` | Runtime scripting for Android-based signage |

## MkDocs Markdown Extensions

The following extensions are enabled and available for use in documentation:

- `admonition` / `markdown.extensions.admonition` - Note/warning/tip callout blocks
- `pymdownx.details` - Collapsible content blocks
- `pymdownx.superfences` - Enhanced fenced code blocks
- `pymdownx.inlinehilite` - Inline code syntax highlighting
- `pymdownx.snippets` - Include content from other files

## Development Commands

```bash
# Install dependencies
pip install mkdocs mkdocs-material

# Serve locally with hot reload
mkdocs serve

# Build the static site (outputs to docs/)
mkdocs build
```

## Conventions

- All documentation source files are Markdown (`.md`) in the `mkdocs/` directory.
- Images go in `mkdocs/img/`.
- The `docs/` directory is the built output and is committed to the repo for GitHub Pages hosting. After editing source files in `mkdocs/`, run `mkdocs build` to regenerate `docs/`.
- Navigation order is defined in the `nav` section of `mkdocs.yml`.
- Use admonitions (`!!! note`, `!!! warning`, `!!! tip`) for callouts.
- Use fenced code blocks with language identifiers for syntax highlighting.
- The site uses the Material theme with the Revel Digital logo (`mkdocs/img/logo.png`).
