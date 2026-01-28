# Layout Settings

Configure card sizes, grid layouts, and responsive behavior.

## Accessing Settings

Go to **MindfulMedia → Settings → Layout**

## Card Dimensions

### Video Cards

| Setting | Default | Description |
|---------|---------|-------------|
| Width | 1920px | Maximum width |
| Height | 1080px | Maximum height |

**Note:** These are maximum dimensions. Cards scale responsively.

### Audio Cards

| Setting | Default | Description |
|---------|---------|-------------|
| Width | 1000px | Maximum width |
| Height | 1000px | Maximum height |

Audio cards can use different ratios (often square for album art).

## Grid Layout

### Items Per Row

| Setting | Default | Description |
|---------|---------|-------------|
| Items Per Row | 5 | Number of cards in a row (desktop) |

### Responsive Breakpoints

The grid automatically adjusts:

| Breakpoint | Columns |
|------------|---------|
| 1200px+ | Items Per Row setting |
| 992px-1199px | 4 columns |
| 768px-991px | 3 columns |
| 576px-767px | 2 columns |
| <576px | 1 column |

### Card Gap

| Setting | Default | Description |
|---------|---------|-------------|
| Card Gap | 16px | Space between cards |

## Featured Section

### Display Options

| Setting | Default | Description |
|---------|---------|-------------|
| Show Featured | Yes | Display featured section |
| Featured Count | 3 | Number of featured items |

### Featured Layout

Featured items display in a hero row at the top:

- Larger thumbnails
- More prominent titles
- Auto-scrolling (optional)

## Slider Settings

### Row Behavior

| Setting | Default | Description |
|---------|---------|-------------|
| Items Visible | 5 | Items visible at once |
| Scroll Amount | 3 | Items to scroll per click |

### Navigation

| Setting | Default | Description |
|---------|---------|-------------|
| Show Arrows | Yes | Show navigation arrows |
| Arrow Style | Chevron | Clean arrow icons |

## CSS Customization

### Card Styling

```css
/* Card container */
.mindful-media-card {
    border-radius: 12px;
    overflow: hidden;
}

/* Card thumbnail */
.mindful-media-card-thumbnail {
    aspect-ratio: 16/9;
}

/* Card title */
.mindful-media-card-title {
    font-size: 14px;
    font-weight: 500;
}
```

### Grid Styling

```css
/* Grid container */
.mindful-media-grid {
    display: grid;
    gap: 16px;
    grid-template-columns: repeat(5, 1fr);
}

/* Responsive override */
@media (max-width: 992px) {
    .mindful-media-grid {
        grid-template-columns: repeat(3, 1fr);
    }
}
```

## Layout Patterns

### YouTube Style

Default layout mimics YouTube:

- 16:9 thumbnails
- Clean card design
- 5 columns on desktop
- Responsive scaling

### Netflix Style

For horizontal sliders:

- Row-based layout
- Horizontal scrolling
- Category headers
- Large thumbnails

### Grid Gallery

For archive pages:

- Uniform grid
- Filter chips above
- Pagination below
- Consistent card sizes

## Best Practices

### Desktop

- 4-5 items per row works well
- Ensure thumbnails are large enough to see
- Keep card text readable

### Tablet

- 3-4 items per row
- Touch-friendly spacing
- Slightly larger touch targets

### Mobile

- 1-2 items per row
- Full-width cards work best
- Swipe-friendly navigation
