# Copy Code Button

> A lightweight WordPress plugin that automatically adds a one-click Copy button to every code block on your site — no configuration required.

[![License: GPL v2](https://img.shields.io/badge/License-GPL%20v2-blue.svg)](https://www.gnu.org/licenses/gpl-2.0.html)
[![WordPress](https://img.shields.io/badge/WordPress-5.9%2B-blue)](https://wordpress.org)
[![PHP](https://img.shields.io/badge/PHP-7.4%2B-blue)](https://php.net)

---

## Features

- Detects code blocks automatically — no template editing
- Supports PrismJS, Highlight.js, Gutenberg, Enlighter, CodeMirror, `<pre>`, `<code>`
- Configurable button text / copied text / failed text / reset time
- Four button positions (top-right, top-left, bottom-right, bottom-left)
- Dark / Light / Auto colour mode
- Show always or show on hover
- Clipboard API + execCommand fallback
- Smart asset loading (JS only runs if code blocks exist)
- Keyboard accessible, ARIA-labelled, focus styles
- Custom CSS selector & exclude selector
- Custom CSS field
- Developer mode
- Zero dependencies — no jQuery, no Bootstrap, no CDN

---

## Screenshots

> _(Add screenshots to `/assets/screenshots/` in the repo)_

| Light mode | Dark mode | Settings page |
|-----------|-----------|--------------|
| ![Light]() | ![Dark]() | ![Settings]() |

---

## Installation

### From ZIP

1. Download the latest release.
2. Go to **Plugins → Add New → Upload Plugin**.
3. Upload the ZIP and activate.

### Manual

```bash
git clone https://github.com/nrwindia/copy-code-button.git \
  wp-content/plugins/copy-code-button
```

Then activate from **Plugins → Installed Plugins**.

---

## Usage

After activation the plugin works automatically. Visit **Settings → Copy Code Button** to customise behaviour.

---

## Supported Plugins / Libraries

| Library | Supported |
|---------|-----------|
| PrismJS | ✅ |
| Highlight.js | ✅ |
| Gutenberg Code Block | ✅ |
| Enlighter | ✅ |
| CodeMirror | ✅ |
| Generic `<pre>` | ✅ |
| Standalone `<code>` | ✅ (opt-in) |

---

## Settings Reference

| Tab | Setting | Default |
|-----|---------|---------|
| General | Enable Plugin | On |
| General | Button Text | Copy |
| General | Copied Text | Copied! |
| General | Failed Text | Failed |
| General | Reset Time (ms) | 2000 |
| General | Fade Animation | On |
| General | Show Button Always | Off (hover) |
| Appearance | Button Position | Top Right |
| Appearance | Dark Mode | Auto |
| Appearance | Border Radius (px) | 6 |
| Appearance | Font Size (px) | 12 |
| Appearance | Button Padding | 4px 8px |
| Appearance | Custom CSS | — |
| Compatibility | Support PRE | On |
| Compatibility | Support CODE | Off |
| Compatibility | Support PrismJS | On |
| Compatibility | Support Highlight.js | On |
| Compatibility | Support Gutenberg | On |
| Compatibility | Support Enlighter | On |
| Compatibility | Support CodeMirror | On |
| Compatibility | Custom CSS Selector | — |
| Compatibility | Exclude CSS Selector | — |
| Advanced | Smart Asset Loading | On |
| Advanced | Clipboard API Fallback | On |
| Advanced | Developer Mode | Off |

---

## Folder Structure

```
copy-code-button/
├── copy-code-button.php   # Main plugin file
├── uninstall.php          # Clean up on uninstall
├── readme.txt             # WordPress Plugin Directory readme
├── README.md              # This file
├── assets/
│   ├── css/
│   │   ├── style.css      # Frontend styles
│   │   └── admin.css      # Admin styles
│   └── js/
│       └── script.js      # Frontend logic
├── includes/
│   ├── loader.php         # Bootstrap / DI
│   ├── helpers.php        # Settings helpers & sanitisation
│   ├── frontend.php       # Asset enqueueing & config
│   ├── admin.php          # Admin menu & settings registration
│   └── settings-page.php  # Settings page HTML
└── languages/             # Translation files (.pot / .po / .mo)
```

---

## Hooks

### Actions

```php
// Fired just before code is copied (JS custom event, PHP counterpart for server-side usage)
do_action( 'copy_code_button_before_copy' );

// Fired after copy attempt
do_action( 'copy_code_button_after_copy' );
```

### Filters

```php
// Modify button label strings
add_filter( 'copy_code_button_text', function( $labels ) {
    $labels['copy'] = 'Clone';
    return $labels;
} );

// Modify button position
add_filter( 'copy_code_button_position', fn() => 'bottom-right' );

// Add / remove CSS selectors
add_filter( 'copy_code_button_selectors', function( $selectors ) {
    $selectors[] = '.my-custom-code';
    return $selectors;
} );

// Modify custom CSS output
add_filter( 'copy_code_button_css', function( $css ) {
    return $css . '.ccb-btn { font-weight: bold; }';
} );
```

---

## Development

```bash
# Clone
git clone https://github.com/nrwindia/copy-code-button.git

# No build step required — vanilla PHP, JS, CSS only
```

Coding standard: [WordPress Coding Standards](https://developer.wordpress.org/coding-standards/).

---

## Contributing

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/my-feature`.
3. Commit your changes following WPCS.
4. Open a Pull Request.

---

## License

GPL v2 or later — see [LICENSE](https://www.gnu.org/licenses/gpl-2.0.html).

---

## Author

**NRW India** — [https://wp.nrwone.in](https://wp.nrwone.in)

---

## Roadmap

- [ ] REST API endpoint for settings
- [ ] Per-block exclude via data attribute
- [ ] Line-number copy option
- [ ] Copy icon SVG option
- [ ] Multisite support
- [ ] WP-CLI commands

---

## FAQ

**Q: Does it conflict with caching plugins?**  
A: No. The button is injected client-side after the cached HTML is delivered.

**Q: Can I use it with a custom theme?**  
A: Yes. Any theme that outputs `<pre>` or `<code>` tags is supported.

**Q: Is it GDPR compliant?**  
A: Yes. No external requests, no tracking, no cookies.

---

## Changelog

### 1.0.0
- Initial release
