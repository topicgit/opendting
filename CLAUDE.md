# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This repository is a single-file static navigation page. The app lives entirely in `index.html`, with HTML structure, CSS styling, and JavaScript behavior all embedded inline. There is no package manager, bundler, framework, or automated test setup in the current snapshot.

## Important Files

- `index.html` — the entire application: page structure, theme styles, section/card content, and client-side interactions.
- `AGENTS.md` — existing repository guidance; keep it aligned if workflows change.
- `.idea/` — IDE metadata only, not application source.

## Development Commands

- `open index.html` — open the page directly in the default macOS browser.
- `python3 -m http.server 8000` — serve the repository locally at `http://localhost:8000` for browser testing.

## Testing

There is no automated test suite.

Manual verification after changes:
- Reload the page and verify the edited sections/cards render correctly.
- Test theme switching and confirm the choice persists via `localStorage` key `nav-theme`.
- Test search filtering: cards should hide/show based on name or description matches, and empty sections should disappear.
- Test Enter in the search box and the search button; both should open a Google search for the current query.
- Recheck desktop and narrow mobile viewport behavior.

## Architecture

### Single-file app model

The page is intentionally self-contained. Future edits will usually happen in one of these inline blocks inside `index.html`:
- the main `<style>` block in `<head>` for layout, theme tokens, cards, and responsive rules
- the `<main>` markup for section/card content
- the bottom `<script>` block for all interactivity
- the final small `<style>` block for the ripple keyframes

### UI structure

The document is organized as:
- fixed theme toggle button
- header with title/subtitle
- search bar
- `<main>` containing repeated `.section` blocks
- footer

Each content section contains a `.section-header` and a `.grid` of anchor-based `.card` entries. Cards are plain links, so adding or editing content usually means editing the repeated card markup rather than wiring new components.

### Styling model

The styling is token-driven through CSS custom properties on `:root`, with light theme overrides on `:root.light`. Theme changes work by toggling the `light` class on `document.documentElement`, so any new styles should use the existing CSS variables instead of hard-coded colors when possible.

### Behavior model

All runtime behavior is plain DOM scripting:
- `applyTheme(theme)` updates the root class and persists the selected theme in `localStorage`.
- Initial theme selection prefers saved state, then falls back to `prefers-color-scheme`.
- Search filtering listens to the search input, hides non-matching `.card` nodes, then hides `.section` blocks whose cards are all hidden.
- `doSearch()` opens a Google search for the current query; it is used by both the search button and the Enter key handler.
- Ripple feedback is added by attaching click listeners to every `.card` and injecting a temporary `<span>` for the animation.

## Editing Guidance

- Keep HTML, CSS, and JS changes localized inside `index.html` unless the user explicitly asks for a multi-file refactor.
- Preserve the current 2-space indentation style.
- Keep UI copy concise and consistent with the current Chinese-language interface.
- When adding sections or cards, follow the existing `.section` / `.grid` / `.card` structure so search and ripple behavior continue to work without extra JavaScript changes.
