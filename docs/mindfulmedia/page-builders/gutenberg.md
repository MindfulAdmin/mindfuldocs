# Gutenberg Blocks

MindfulMedia provides 4 Gutenberg blocks for the WordPress block editor.

## Finding the Blocks

1. Edit a page with Gutenberg
2. Click **+** to add a block
3. Search for "MindfulMedia" or "mindful"
4. Select from available blocks

All blocks appear under the **MindfulMedia** category.

## Available Blocks

| Block | Purpose |
|-------|---------|
| MindfulMedia Browse | Full browse page layout |
| MindfulMedia Archive | Media grid with filters |
| MindfulMedia Embed | Single media or playlist |
| MindfulMedia Category Row | Horizontal slider |

---

## MindfulMedia Browse

Creates a full browse experience with navigation tabs and category sections.

### Block Settings

| Setting | Options |
|---------|---------|
| Show Featured | Yes / No |
| Show Navigation | Yes / No |
| Sections | Multi-select: Teachers, Topics, Playlists, Categories |

### Usage

Best for:

- Media landing page
- Browse page
- Main media hub

### Equivalent Shortcode

```html
[mindful_media_browse]
```

---

## MindfulMedia Archive

Displays a filterable grid of media items.

### Block Settings

| Setting | Options |
|---------|---------|
| Items Per Page | Number input |
| Show Filters | Yes / No |
| Show Pagination | Yes / No |
| Category Filter | Dropdown selection |
| Topic Filter | Dropdown selection |
| Teacher Filter | Dropdown selection |
| Media Type | All / Audio / Video |
| Featured Only | Yes / No |

### Usage

Best for:

- Media archive page
- Category-specific pages
- Search results page

### Equivalent Shortcode

```html
[mindful_media_archive per_page="12" topic="meditation"]
```

---

## MindfulMedia Embed

Embeds a single media item or playlist.

### Block Settings

| Setting | Options |
|---------|---------|
| Source | Media Item / Playlist |
| Media Item | Dropdown or ID input |
| Playlist | Dropdown selection |
| Size | Small / Medium / Large / Full Width |
| Autoplay | Yes / No |

### Size Options

| Size | Width |
|------|-------|
| Small | 320px |
| Medium | 560px |
| Large | 800px |
| Full Width | 100% |

### Usage

Best for:

- Embedding specific videos in posts
- Course landing pages
- Featured content sections

### Equivalent Shortcode

```html
[mindful_media id="123" size="large"]
[mindful_media playlist="beginner-course"]
```

---

## MindfulMedia Category Row

Displays a Netflix-style horizontal slider of taxonomy terms.

### Block Settings

| Setting | Options |
|---------|---------|
| Taxonomy | Teachers / Topics / Categories / Playlists |
| Title | Custom text (optional) |
| Items to Show | Number input |
| Show "View All" Link | Yes / No |

### Usage

Best for:

- Homepage sections
- Category highlights
- Featured teachers/topics

### Equivalent Shortcode

```html
[mindful_media_row taxonomy="media_topic" title="Browse by Topic"]
```

---

## Block Tips

### Server-Side Rendering

All MindfulMedia blocks use server-side rendering:

- Preview in editor shows actual content
- Styling matches frontend exactly
- Changes reflect immediately on save

### Combining Blocks

Create rich layouts by combining blocks:

```
[Hero Section with Embed Block - Full Width]

[Category Row - Featured Teachers]

[Archive Block - Latest Videos]

[Category Row - Popular Topics]
```

### Column Layouts

Embed blocks work great in columns:

1. Add a Columns block
2. Add MindfulMedia Embed to each column
3. Set appropriate sizes

### Full Width Pages

For best results:

1. Use a full-width page template
2. Or use a page builder with sections
3. Remove sidebar for media pages

## Styling Blocks

### Block Spacing

Add custom spacing using the Spacer block or block settings.

### Background Colors

Wrap in a Group block to add backgrounds:

1. Add Group block
2. Set background color
3. Add MindfulMedia block inside

### Custom CSS

Target blocks with:

```css
/* All MindfulMedia blocks */
.wp-block-mindful-media {
    /* Your styles */
}

/* Specific blocks */
.wp-block-mindful-media-browse {
    /* Browse block styles */
}

.wp-block-mindful-media-archive {
    /* Archive block styles */
}
```

## Troubleshooting

### Block Not Appearing

1. Clear browser cache
2. Deactivate/reactivate plugin
3. Check for JavaScript errors

### Preview Not Loading

1. Check AJAX is working
2. Verify no PHP errors
3. Clear plugin transients

### Styling Issues

1. Check theme compatibility
2. Try with default theme
3. Inspect for CSS conflicts
