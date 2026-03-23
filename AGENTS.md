# Agent Instructions for "El Jardín de Mi Amor"

This is a vanilla HTML/CSS/JavaScript project for an interactive birthday gift web application. It uses Tailwind CSS via CDN and Google Fonts.

## Project Overview

- **Type**: Interactive web gift (single-page application)
- **Tech Stack**: HTML5, CSS3, Vanilla JavaScript, Tailwind CSS (CDN)
- **Main File**: `index.html` (all code is self-contained)

## Build/Run Commands

Since this is a vanilla HTML project, there is no build process required.

### Running the Application

```bash
# Open directly in browser
start index.html          # Windows
open index.html           # macOS
xdg-open index.html       # Linux
```

### Testing

There are no automated tests configured. Manual testing should include:
- Opening `index.html` in multiple browsers (Chrome, Firefox, Safari, Edge)
- Testing responsive layouts at different viewport sizes (mobile, tablet, desktop)
- Verifying all 28 daisies are clickable and open modals
- Testing the counter updates correctly
- Verifying the celebration modal triggers at 28/28

### Linting

No linter is configured. Code should follow the style guidelines below.

### Development

For live development with auto-refresh:
```bash
# Using Python's HTTP server
python -m http.server 8000

# Or using Node.js
npx serve .
```

Then visit `http://localhost:8000`

## Code Style Guidelines

### General Principles

1. **Single File Architecture**: All HTML, CSS, and JavaScript lives in `index.html`
2. **No Build Step**: Avoid requiring npm/webpack/vite for this project
3. **Progressive Enhancement**: Core functionality works without JavaScript
4. **Accessibility**: Include ARIA labels, keyboard navigation, focus states

### HTML Guidelines

- Use semantic HTML5 elements (`<header>`, `<main>`, `<section>`, `<button>`)
- Always include `viewport` meta tag for responsive design
- Use `clamp()` for responsive font sizes: `font-size: clamp(1rem, 2.5vw, 1.5rem)`
- Include `lang="es"` for Spanish content
- Use kebab-case for class names

### CSS Guidelines

#### Variables
- Define CSS custom properties in `:root` at the top of `<style>`
- Use semantic variable names reflecting purpose, not color values
- Group related variables together

```css
:root {
    /* Colors */
    --azul-noche: #1a1a2e;
    --bronce: #c9a227;
    --oro-estelar: #ffd700;
    
    /* Typography */
    --font-display: 'Cinzel Decorative', serif;
    --font-body: 'EB Garamond', serif;
}
```

#### Selectors
- Prefer class selectors over element selectors
- Use BEM-lite naming: `.component-element--modifier`
- Avoid `!important` except for utility overrides

#### Animations
- Use CSS animations over JavaScript where possible
- Support `prefers-reduced-motion`:
```css
@media (prefers-reduced-motion: reduce) {
    *, *::before, *::after {
        animation-duration: 0.01ms !important;
        transition-duration: 0.01ms !important;
    }
}
```
- Define keyframes at top of `<style>` block
- Use CSS custom properties for animation timing

#### Responsive Design
- Use mobile-first approach
- Define breakpoints at 768px (tablet) and 1024px (desktop)
- Test touch interactions on mobile

### JavaScript Guidelines

#### Configuration Section
- Place all customizable data at the top of `<script>`
- Use `const` for arrays and objects
- Document each configuration array with comments

```javascript
// ============================================
// CONFIGURACIÓN - PERSONALIZA AQUÍ
// ============================================

const POEMS = [
    "Poema 1...",
    // Add more poems...
];

const SETTINGS = {
    daisyCount: 28,
    celebrationEnabled: true
};
```

#### State Management
- Use a single state object to track application state
- Initialize state with sensible defaults
- Save state to localStorage when needed

```javascript
const state = {
    collected: new Set(),
    isModalOpen: false,
    currentPoemIndex: null,
    celebrationTriggered: false
};
```

#### Functions
- Use descriptive, camelCase function names
- Keep functions small and focused (single responsibility)
- Document complex functions with comments

```javascript
function collectDaisy(id) {
    if (state.collected.has(id) || state.isModalOpen) return;
    
    state.collected.add(id);
    saveProgress();
    createSparkles(daisy);
    updateCounter();
    openModal(id);
    
    if (state.collected.size >= 28) {
        setTimeout(triggerCelebration, 1000);
    }
}
```

#### Event Handling
- Use `addEventListener` instead of inline handlers where possible
- Support keyboard navigation (Escape to close modals)
- Debounce rapid clicks to prevent double-triggers

#### DOM Manipulation
- Use `document.getElementById()` for specific elements
- Use `classList` for toggling classes
- Cache DOM references for frequently accessed elements

```javascript
const counterBadge = document.getElementById('counterBadge');

function updateCounter() {
    countNumber.textContent = state.collected.size;
    counterBadge.classList.add('bounce');
    setTimeout(() => counterBadge.classList.remove('bounce'), 300);
}
```

### SVG Guidelines

- Use inline SVGs for icons and graphics
- Define consistent viewBox sizes
- Use currentColor for fill/stroke to support theming
- Optimize paths (remove unnecessary precision)

### Naming Conventions

| Element | Convention | Example |
|---------|------------|---------|
| CSS Variables | kebab-case | `--azul-noche` |
| CSS Classes | kebab-case | `.daisy-collected` |
| JavaScript Functions | camelCase | `collectDaisy()` |
| JavaScript Constants | SCREAMING_SNAKE_CASE | `ROMAN_NUMERALS` |
| JavaScript State | camelCase | `isModalOpen` |
| IDs | kebab-case | `daisy-0` |

### Error Handling

- Return early for invalid states
- Check for null/undefined before accessing properties
- Use console warnings for non-critical issues
- Never expose sensitive information in console logs

### Performance Considerations

- Use `transform` and `opacity` for animations (GPU accelerated)
- Limit DOM manipulation in loops
- Use `requestAnimationFrame` for complex animations
- Lazy-load images with `loading="lazy"`
- Minimize repaints and reflows

## File Structure

```
el jardin de mi amor/
├── index.html          # Main application (HTML + CSS + JS)
├── SPEC.md             # Creative specification document
└── AGENTS.md           # This file
```

## Common Tasks

### Adding a New Daisy Position
Edit the `DAISY_POSITIONS` array:
```javascript
{ x: 50, y: 50, rot: 0, scale: 1 }
```

### Adding a New Poem
Update the `POEMS` array at line ~300 in index.html:
```javascript
const POEMS = [
    "Tu poema aquí...",
    // ... existing poems
];
```

### Testing the Celebration Modal
Run in browser console:
```javascript
triggerCelebration();
```

### Resetting Progress
```javascript
localStorage.removeItem('krismarGarden');
location.reload();
```

## Version Control

- Commit messages should be in Spanish or English
- Keep commits focused on single features/changes
- Include relevant context in commit descriptions
