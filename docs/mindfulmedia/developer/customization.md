# CSS Customization

MindfulMedia uses CSS variables and well-structured classes for easy theming.

## CSS Variables

### Defining Custom Colors

Override in your theme's CSS:

```css
:root {
    /* Primary branding */
    --mindful-media-primary: #8B0000;
    --mindful-media-secondary: #DAA520;
    
    /* Text colors */
    --mindful-media-text-light: #FFFFFF;
    --mindful-media-text-dark: #333333;
    
    /* Player colors */
    --mindful-media-progress-color: #ff0000;
}
```

### Light Theme Variables

Used on browse/archive pages:

```css
:root {
    --mm-bg-primary: #ffffff;
    --mm-bg-secondary: #f2f2f2;
    --mm-text-primary: #0f0f0f;
    --mm-text-secondary: #606060;
    --mm-border-color: #e5e5e5;
}
```

### Dark Theme Variables

Used in modal player and single pages:

```css
:root {
    --mm-dark-bg-primary: #0f0f0f;
    --mm-dark-bg-secondary: #212121;
    --mm-dark-text-primary: #f1f1f1;
    --mm-dark-text-secondary: #aaaaaa;
    --mm-dark-border-color: #3f3f3f;
}
```

### Z-Index Scale

```css
:root {
    --mm-z-base: 1;           /* Cards, default elements */
    --mm-z-dropdown: 100;     /* Dropdowns, menus */
    --mm-z-sticky: 500;       /* Sticky headers */
    --mm-z-overlay: 1000;     /* Overlays, backdrops */
    --mm-z-modal: 10000;      /* Modal dialogs */
    --mm-z-modal-content: 10001;  /* Modal controls */
    --mm-z-toast: 99999;      /* Notifications */
}
```

---

## Key CSS Classes

### Containers

| Class | Description |
|-------|-------------|
| `.mindful-media-container` | Main wrapper |
| `.mindful-media-archive` | Archive grid container |
| `.mindful-media-browse` | Browse page container |
| `.mindful-media-single` | Single page wrapper |
| `.mindful-media-inline-player` | Modal player container |

### Cards

| Class | Description |
|-------|-------------|
| `.mindful-media-card` | Individual card |
| `.mindful-media-card-thumbnail` | Card thumbnail |
| `.mindful-media-card-title` | Card title |
| `.mindful-media-card-meta` | Card metadata |
| `.mindful-media-duration-badge` | Duration display |

### Player

| Class | Description |
|-------|-------------|
| `.mindful-media-player-container` | Player wrapper |
| `.mindful-media-player-aspect-ratio` | Aspect ratio container |
| `.mindful-media-audio-controls` | Audio player controls |
| `.mindful-media-progress-bar` | Progress bar |

### Engagement

| Class | Description |
|-------|-------------|
| `.mm-like-btn` | Like button |
| `.mm-subscribe-btn` | Subscribe button |
| `.mm-comments-section` | Comments container |
| `.mm-engagement-section` | Engagement wrapper |

### Navigation

| Class | Description |
|-------|-------------|
| `.mm-nav-tabs` | Tab navigation |
| `.mm-nav-tab` | Individual tab |
| `.mindful-media-filter-chips` | Filter chips container |
| `.mm-chip` | Filter chip |

---

## Customization Examples

### Custom Card Style

```css
/* Rounded cards with shadow */
.mindful-media-card {
    border-radius: 16px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    transition: transform 0.2s, box-shadow 0.2s;
}

.mindful-media-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
}
```

### Custom Progress Bar

```css
/* Gradient progress bar */
.mindful-media-progress-bar {
    height: 6px;
    border-radius: 3px;
    background: linear-gradient(
        to right,
        var(--mindful-media-primary),
        var(--mindful-media-secondary)
    );
}
```

### Custom Button Styles

```css
/* Like button */
.mm-like-btn {
    padding: 8px 16px;
    border-radius: 20px;
    background: transparent;
    border: 1px solid currentColor;
    transition: all 0.2s;
}

.mm-like-btn:hover {
    background: rgba(255, 0, 0, 0.1);
}

.mm-like-btn.liked {
    background: #ff0000;
    color: white;
    border-color: #ff0000;
}
```

### Custom Filter Chips

```css
/* Pill-shaped filter chips */
.mm-chip {
    padding: 10px 20px;
    border-radius: 25px;
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 0.5px;
}

.mm-chip.active {
    background: var(--mindful-media-primary);
    color: white;
}
```

---

## Dark Mode Support

### Auto Dark Mode

Add class to enable system dark mode:

```html
<div class="mindful-media-container mm-auto-dark-mode">
    <!-- Content uses dark theme when OS prefers dark -->
</div>
```

### Manual Dark Mode

Force dark theme:

```css
.my-dark-section .mindful-media-container {
    --mm-bg-primary: var(--mm-dark-bg-primary);
    --mm-bg-secondary: var(--mm-dark-bg-secondary);
    --mm-text-primary: var(--mm-dark-text-primary);
    --mm-text-secondary: var(--mm-dark-text-secondary);
}
```

---

## Responsive Customization

### Breakpoint Variables

```css
/* Custom breakpoints */
@media (max-width: 1200px) {
    .mindful-media-grid {
        grid-template-columns: repeat(4, 1fr);
    }
}

@media (max-width: 992px) {
    .mindful-media-grid {
        grid-template-columns: repeat(3, 1fr);
    }
}

@media (max-width: 768px) {
    .mindful-media-grid {
        grid-template-columns: repeat(2, 1fr);
    }
    
    .mindful-media-card-title {
        font-size: 13px;
    }
}

@media (max-width: 576px) {
    .mindful-media-grid {
        grid-template-columns: 1fr;
    }
}
```

### Mobile-Specific Styles

```css
@media (max-width: 768px) {
    /* Full-width cards on mobile */
    .mindful-media-card {
        margin: 0 -16px;
        border-radius: 0;
    }
    
    /* Larger touch targets */
    .mm-like-btn,
    .mm-subscribe-btn {
        min-height: 44px;
        min-width: 44px;
    }
    
    /* Stack engagement buttons */
    .mm-engagement-section {
        flex-direction: column;
        gap: 12px;
    }
}
```

---

## Template Overrides

### Override Templates

Copy template files to your theme:

```
your-theme/
└── mindfulmedia/
    ├── single-mindful-media.php
    ├── taxonomy-media_series.php
    ├── taxonomy-media_teacher.php
    └── taxonomy-media_topic.php
```

The plugin checks your theme first, then falls back to plugin templates.

### Template Parts

Create partial templates:

```php
// In your theme template
<?php 
// Custom card partial
get_template_part('mindfulmedia/card', 'custom');
?>
```

---

## JavaScript Hooks

### Custom Events

Listen for plugin events:

```javascript
// When modal opens
document.addEventListener('mindful-media-modal-open', function(e) {
    console.log('Modal opened for:', e.detail.postId);
});

// When video completes
document.addEventListener('mindful-media-complete', function(e) {
    console.log('Video completed:', e.detail.postId);
});

// When user likes
document.addEventListener('mindful-media-liked', function(e) {
    console.log('User liked:', e.detail.postId);
});
```

### Extend JavaScript

```javascript
// Add after mindful-media-frontend.js loads
jQuery(document).ready(function($) {
    // Custom initialization
    $('.mindful-media-card').each(function() {
        // Add custom behavior
    });
});
```

---

## Print Styles

The plugin includes print-optimized CSS:

```css
@media print {
    /* Hide interactive elements */
    .mindful-media-inline-player,
    .mm-like-btn,
    .mm-subscribe-btn,
    .mindful-media-filter-chips {
        display: none !important;
    }
    
    /* Convert grid to list */
    .mindful-media-grid {
        display: block;
    }
    
    .mindful-media-card {
        page-break-inside: avoid;
        margin-bottom: 20px;
    }
}
```

---

## Best Practices

### Specificity

Use plugin classes for specificity without `!important`:

```css
/* Good - specific selector */
.mindful-media-container .mindful-media-card {
    border-radius: 16px;
}

/* Avoid if possible */
.mindful-media-card {
    border-radius: 16px !important;
}
```

### Performance

- Minimize custom CSS
- Use CSS variables for theme changes
- Avoid complex selectors
- Test on mobile devices

### Compatibility

- Test with your theme
- Check for conflicts
- Use browser dev tools
- Validate responsive behavior
