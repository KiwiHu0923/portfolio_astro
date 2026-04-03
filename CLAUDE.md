# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Flask-based portfolio website showcasing personal projects. The site uses server-side rendering with Jinja2 templates and serves static content including a PDF resume.

## Architecture

### Core Application Structure

- **Main application**: [\_\_init\_\_.py](__init__.py) - Contains all Flask routes and application logic
- **Project data**: [projects.json](projects.json) - JSON file serving as the project database (lazy loaded on each request)
- **Templates**: `templates/` directory with Jinja2 HTML files
  - [base.html](templates/base.html) - Base template with header navigation and footer
  - [home.html](templates/home.html) - Project listing page (extends base)
  - Individual project pages follow the pattern `project_{slug}.html`
  - [404.html](templates/404.html) - Custom error page
- **Static assets**: `static/` directory containing CSS, images, and Resume.pdf

### Key Design Patterns

**Project System**: Projects are stored in [projects.json](projects.json) with the following structure:
```json
{
  "name": "Project Name",
  "thumb": "img/thumbnail.svg",
  "hero": "img/hero.png",
  "categories": ["category1", "category2"],
  "slug": "project-slug"
}
```

The `slug` field maps to a corresponding template file `templates/project_{slug}.html`. Each project page contains its own hardcoded content rather than storing descriptions in the JSON.

**Template Inheritance**: All pages extend [base.html](templates/base.html) using `{% extends "base.html" %}` and override the `content` block. The base template includes navigation with active link highlighting based on `request.path`.

**Database Migration**: The codebase previously used MongoDB (see git history) but was migrated to use JSON for simplicity. The `.env.example` still references `MONGODB_URI` but it's no longer used.

## Development Commands

### Setup
```bash
# Install dependencies
pip install -r requirements.txt

# Install development tools (black, flake8)
pip install -r requirements-dev.txt

# Create environment file (currently only needed for legacy MongoDB reference)
cp .env.example .env
```

### Running the Application
```bash
# Development server
flask --app __init__ run

# Production server with gunicorn
gunicorn __init__:app
```

### Code Quality
```bash
# Format code
black __init__.py

# Lint code
flake8 __init__.py
```

## Adding New Projects

1. Add project metadata to [projects.json](projects.json) with a unique `slug`
2. Create corresponding template file at `templates/project_{slug}.html`
3. Ensure the template extends `base.html` and implements the `content` block
4. Place thumbnail image at path specified in `thumb` field/
5. Place hero image at path specified in `hero` field (both relative to `static/` directory)

## Important Notes

- The navigation in [base.html](templates/base.html) uses `url_for()` for dynamic URL generation
- Active navigation links are highlighted using conditional class `nav__link--active`
- Resume is served directly from `static/Resume.pdf` via [\_\_init\_\_.py:34](__init__.py#L34)
- Comments in templates are in Chinese, providing context for Jinja2 patterns
- Project data is loaded fresh on each request (no caching) via `get_projects()`
