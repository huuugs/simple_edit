# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a single-file Chinese notepad application (记事本) built as a self-contained HTML file with embedded CSS and JavaScript. The application is a modern web-based text editor with Chinese localization and advanced features.

## Architecture

### Single-File Structure
- **index.html**: Contains the entire application (HTML, CSS, JavaScript)
- No external dependencies, build process, or installation required
- Self-contained with UTF-8 Chinese language support

### Core Application
- **Notepad class** (lines 2069-4034): Main application controller
- **Initialization**: `document.addEventListener('DOMContentLoaded'()` creates `window.notepadApp`
- **Storage**: LocalStorage for settings persistence and auto-save
- **Theme system**: CSS custom properties with dark/light mode support

### Key Components
- **Editor**: Main text editing area with real-time statistics
- **Toolbar**: File operations, text formatting, search/replace
- **Modals**: Settings, help, and confirmation dialogs
- **Mobile UI**: Responsive design with touch-friendly controls

## Development Commands

### Running the Application
```bash
# Serve with Python (recommended)
python3 -m http.server 8000

# Serve with Node.js
npx serve .

# Direct browser opening (works but may have CORS issues)
# Open index.html directly in a web browser
```

### Git Workflow
```bash
# Current state: Repository initialized, no commits
git add index.html
git commit -m "Initial commit: Chinese notepad application"
```

### Testing
- **Manual testing**: Open in browser and test functionality
- **Mobile testing**: Test responsive design on mobile browsers
- **No automated tests**: No test framework currently configured

## Key Features

### Advanced Search & Replace
- High-performance find/replace with intelligent result caching
- Chinese/English whole-word matching with Unicode-aware regex
- Case-sensitive search with optimized navigation (find next/prev)
- Smart positioning and viewport-aware scrolling
- Comprehensive error handling and input validation
- Performance-optimized for large documents

### Text Operations
- Undo/redo functionality with history management (50-operation limit)
- Markdown formatting support via floating toolbar
- Indent/outdent with tab/shift+tab support
- Word wrap toggle with mobile responsiveness
- Real-time character/word/line statistics

### File Operations
- Save to multiple formats (.txt, .md, .html, .css, .js, .json, .xml, .csv)
- Smart file extension detection based on content
- Open UTF-8 text files
- Auto-save to LocalStorage

### UI Features
- Dark/light theme toggle with CSS custom properties
- Full-screen mode support
- Real-time character/word/line statistics
- Bottom margin adjustment slider
- Mobile-responsive design with touch controls

## Development Guidelines

### Modifying the Application
- Edit `index.html` directly
- Test changes immediately in browser (no build step)
- Check mobile responsiveness after UI changes
- Validate Chinese text displays correctly

### Adding New Features
- Add new methods to the `Notepad` class
- Use CSS custom properties for consistent theming
- Implement modal dialogs for new UI components
- Store new settings in LocalStorage following existing patterns

### Code Conventions
- Chinese language interface throughout
- CSS uses semantic class naming (`.toolbar`, `.editor-container`)
- JavaScript follows ES6+ class-based patterns
- Event delegation for dynamic content handling
- Consistent error handling with user-friendly Chinese messages

### Browser Compatibility
- Works in modern browsers with ES6+ support
- Mobile Safari/Chrome responsive design tested
- Clipboard API with fallbacks for older browsers
- LocalStorage requirement for settings persistence

## Performance Optimizations

### Search Result Caching
- Intelligent caching system using `lastSearchText`, `lastTextLength`, and `lastSearchOptions`
- Avoids expensive regex operations when search conditions haven't changed
- Provides significant performance improvements for repeated searches in large documents
- `selectAndScrollToMatch()` method handles navigation with minimal DOM manipulation

### Smart Scrolling & Viewport Management
- Viewport-aware scrolling only triggers when matches are outside visible area
- Uses precise line-height calculations from `getComputedStyle()` for accurate positioning
- Prevents unnecessary DOM reflows during search navigation
- Mobile viewport optimization using `100dvh` with `100vh` fallback

### Debounced Operations
- Window resize events debounced using `resizeTimeout` (200ms delay)
- Delayed initialization ensures DOM readiness before UI setup
- Efficient event handling prevents performance issues on mobile devices

## Mobile Optimizations

### Dynamic Viewport Handling
- Uses CSS `100dvh` for accurate mobile viewport height accounting
- Falls back to `100vh` for older browser compatibility
- Handles browser UI changes on mobile devices dynamically

### Responsive Features
- Automatic word wrap activation on screens ≤768px via `checkScreenSize()`
- Touch-friendly 38px minimum button targets
- Optimized text selection with `-webkit-touch-callout: default`
- Bottom margin adjustment slider for mobile text entry optimization

## Security & Browser Compatibility

### Clipboard Security
- Checks `window.isSecureContext` before using modern Clipboard API
- Graceful fallback to `document.execCommand('copy')` for non-HTTPS contexts
- Multiple fallback strategies including hidden textarea method ensure cross-browser compatibility

### Progressive Enhancement
- Feature detection before using modern APIs (LocalStorage, Clipboard, etc.)
- Comprehensive fallback methods for older browsers including WebKit-specific properties
- Safe DOM manipulation with consistent null checking

### Safe Data Handling
- JSON.parse() wrapped in try/catch blocks for localStorage preferences
- Error logging for debugging preference loading issues
- Validation of element existence before DOM operations

## Development Best Practices

### Error Handling Patterns
```javascript
// Consistent null checking pattern
if (!this.editor) {
    console.error('Editor element not found');
    return;
}

// Match validation in search operations
if (!match || typeof match.index !== 'number' || !match[0]) {
    console.error('Invalid match object:', match);
    return;
}

// Array bounds checking
if (index < 0 || index >= array.length) {
    this.showMessage('错误', '索引超出范围');
    return;
}
```

### State Management
- Preferences stored as JSON in localStorage with comprehensive error handling
- Undo/redo history management with configurable limit (default: 50 operations)
- Real-time UI updates with efficient debouncing
- Automatic state persistence across browser sessions

### Performance Considerations
- Cache expensive computation results (search results, statistics calculations)
- Use viewport detection to avoid unnecessary DOM operations
- Implement proper cleanup for intervals and timeouts
- Optimize scrolling operations to prevent layout thrashing

## Deployment

- Single file deployment: Upload `index.html` to any web server
- Offline capable: Works completely offline once loaded
- No build step or optimization required
- CDN-free: All assets embedded in HTML file
- HTTPS recommended for full Clipboard API functionality
- to
- t