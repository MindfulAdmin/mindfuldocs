# Elementor Widgets

MindfulMedia provides 4 Elementor widgets for drag-and-drop page building.

## Finding the Widgets

1. Edit a page with Elementor
2. Search for "MindfulMedia" or "mindful"
3. Drag widget to your canvas

All widgets appear under the **MindfulMedia** category in the widget panel.

## Available Widgets

| Widget | Purpose |
|--------|---------|
| MindfulMedia Browse | Full browse page layout |
| MindfulMedia Embed | Single media or playlist |
| MindfulMedia Archive | Media grid with filters |
| MindfulMedia Category Row | Horizontal slider |

---

## MindfulMedia Browse

Creates a complete browse experience with navigation and sections.

### Widget Controls

**Content Tab:**

| Control | Options |
|---------|---------|
| Show Featured | Yes / No |
| Show Navigation | Yes / No |
| Sections | Checkboxes for each section |

### Best For

- Main media library page
- Browse/discovery page
- Media landing page

---

## MindfulMedia Embed

Embeds a single media item or complete playlist.

### Widget Controls

**Content Tab:**

| Control | Options |
|---------|---------|
| Embed Type | Media Item / Playlist |
| Select Media | Dropdown of media items |
| Select Playlist | Dropdown of playlists |
| Embed Size | Small / Medium / Large / Full |
| Autoplay | Yes / No |

**Style Tab:**

| Control | Options |
|---------|---------|
| Alignment | Left / Center / Right |
| Max Width | Slider or custom value |

### Best For

- Embedding videos in posts
- Course/playlist landing pages
- Featured content areas

---

## MindfulMedia Archive

Displays a grid of media items with optional filtering.

### Widget Controls

**Content Tab:**

| Control | Options |
|---------|---------|
| Items Per Page | Number |
| Show Filters | Yes / No |
| Show Pagination | Yes / No |
| Filter by Category | Dropdown |
| Filter by Topic | Dropdown |
| Filter by Teacher | Dropdown |
| Media Type | All / Audio / Video |
| Featured Only | Yes / No |

**Style Tab:**

| Control | Options |
|---------|---------|
| Columns | Slider (1-6) |
| Gap | Slider |

### Best For

- Video archive pages
- Category pages
- Search results

---

## MindfulMedia Category Row

Creates a Netflix-style horizontal slider.

### Widget Controls

**Content Tab:**

| Control | Options |
|---------|---------|
| Taxonomy | Teachers / Topics / Categories / Playlists |
| Custom Title | Text field |
| Items to Show | Number |
| Show View All Link | Yes / No |

**Style Tab:**

| Control | Options |
|---------|---------|
| Title Color | Color picker |
| Title Size | Typography controls |
| Arrow Style | Color and size |

### Best For

- Homepage sections
- Category highlights
- Featured content rows

---

## Building Layouts

### Full Browse Page

```
[Section - Full Width]
└── MindfulMedia Browse Widget

[Section - Call to Action]
└── Your CTA content
```

### Custom Landing Page

```
[Hero Section]
└── MindfulMedia Embed (Featured Playlist, Full Width)

[Content Section]
├── [Column 1/2]
│   └── Text/Heading widgets
└── [Column 1/2]
    └── MindfulMedia Category Row (Topics)

[Archive Section]
└── MindfulMedia Archive (Latest Videos)
```

### Teacher Profile

```
[Hero Section]
├── Image Widget (Teacher Photo)
├── Heading Widget (Teacher Name)
└── Text Widget (Bio)

[Content Section]
└── MindfulMedia Archive (Filter by Teacher)
```

## Styling Tips

### Section Settings

- Use full-width sections for immersive experience
- Set section padding to 0 for edge-to-edge widgets
- Use dark backgrounds for video-focused sections

### Widget Spacing

- Add padding in Advanced tab
- Use margin controls for spacing between widgets
- Consistent spacing throughout page

### Responsive Design

All widgets are responsive by default. Fine-tune with:

1. Switch to tablet/mobile view in Elementor
2. Adjust columns count
3. Modify spacing and sizing

## Custom CSS

### Widget Classes

Each widget has classes you can target:

```css
/* Browse widget */
.elementor-widget-mindful-media-browse {
    /* Your styles */
}

/* Archive widget */
.elementor-widget-mindful-media-archive {
    /* Your styles */
}

/* Embed widget */
.elementor-widget-mindful-media-embed {
    /* Your styles */
}

/* Row widget */
.elementor-widget-mindful-media-row {
    /* Your styles */
}
```

### Custom CSS Control

Add widget-specific CSS in:

1. Select widget
2. Go to Advanced tab
3. Scroll to Custom CSS
4. Add your styles using `selector`

```css
selector {
    border: 2px solid #gold;
}

selector .mindful-media-card {
    border-radius: 16px;
}
```

## Template Library

Save widget configurations as templates:

1. Configure widget perfectly
2. Right-click widget
3. Save as Template
4. Reuse across pages

## Troubleshooting

### Widget Not Found

1. Ensure MindfulMedia is activated
2. Refresh Elementor editor
3. Clear Elementor cache (Dashboard → Elementor → Tools)

### Styling Not Applied

1. Clear Elementor CSS cache
2. Check for CSS conflicts
3. Increase specificity in custom CSS

### Preview Issues

1. Save and preview on frontend
2. Elementor preview may not show all dynamic content
3. Clear browser cache
