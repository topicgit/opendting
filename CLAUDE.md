# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

谛听 (Diting) - 天枢 is a minimalist navigation hub website with Chinese aesthetic design. It features:
- Glass-morphism UI with ink-wash painting style borders
- Dark/light mode toggle with localStorage persistence
- Responsive grid layout for navigation cards
- Search functionality using Google

## Tech Stack

- **HTML5** - Single page application
- **Tailwind CSS** (CDN) - Utility-first CSS framework
- **Font Awesome** (CDN) - Icon library
- **Noto Serif SC** (Google Fonts) - Chinese serif typography
- **Vanilla JavaScript** - Dark mode toggle, search, drag-and-drop sorting

## Architecture

Single HTML file (`index.html`) containing:
- Inline CSS with custom properties for glass-morphism effects
- Embedded JavaScript for interactivity (no build step required)
- All styles and scripts are self-contained

## Key Features

- **Dark mode**: Toggled via `.dark` class on `documentElement`, persisted to localStorage
- **Search**: Google search form embedded in header
- **Drag-and-drop**: Cards can be reordered, positions saved to localStorage
- **Responsive**: Grid adjusts from 1 to 3 columns based on viewport width

## Development

No build process - open `index.html` directly in a browser or serve via any static file server:

```bash
# Simple local server (any option works)
python3 -m http.server 8000
# or
npx serve
```

## Git Workflow

- Default branch: `main`
- No CI/CD configured
- Static site deployment to any static hosting
