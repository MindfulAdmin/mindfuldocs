# Archive & Browse Settings

Configure the media archive and browse page displays.

## Accessing Settings

Go to **MindfulMedia → Settings → Archive & Browse**

## Archive Settings

### Filter Chips

| Setting | Default | Description |
|---------|---------|-------------|
| Show Filter Chips | Yes | Display horizontal filter buttons |
| Show Taxonomy Counts | Yes | Show item counts on filter chips |

### Pagination

| Setting | Default | Description |
|---------|---------|-------------|
| Items Per Page | 12 | Number of items per page |
| Show Pagination | Yes | Display pagination controls |

### Featured Section

| Setting | Default | Description |
|---------|---------|-------------|
| Show Featured | Yes | Display featured items section |
| Featured Count | 3 | Number of featured items |

### Grid Layout

| Setting | Default | Description |
|---------|---------|-------------|
| Items Per Row | 5 | Cards per row on desktop |

## Browse Navigation Tabs

Control which tabs appear on the browse page:

| Tab | Default | Description |
|-----|---------|-------------|
| Home (All) | Yes | Show combined home view |
| Teachers | Yes | Show teachers tab |
| Topics | Yes | Show topics tab |
| Playlists | Yes | Show playlists tab |
| Categories | Yes | Show categories tab |
| Media Types | No | Show audio/video type tabs |

### Tab Labels

Customize the text for each tab (defaults to taxonomy labels).

## Browse Sections

Control which sections appear on the Home tab:

| Section | Default | Description |
|---------|---------|-------------|
| Teachers | Yes | Show teachers slider |
| Topics | Yes | Show topics slider |
| Playlists | Yes | Show playlists slider |
| Categories | Yes | Show categories slider |
| Media Types | No | Show media type filters |

## Navigation URLs

### Browse Page URL

The URL where your `[mindful_media_browse]` shortcode is placed.

**Used for:**

- Home tab navigation
- "Back to Browse" links
- Tab switching redirects

**Example:** `/browse` or `/media-library`

### Media Archive URL

The URL where your `[mindful_media_archive]` shortcode is placed.

**Used for:**

- "View All Media" links
- Breadcrumb navigation
- Archive page redirects

**Example:** `/media` or `/videos`

## Search

### Archive Search

| Setting | Default | Description |
|---------|---------|-------------|
| Show Search | Yes | Display search bar on archive |
| Search Mode | AJAX | Real-time search results |

### Browse Search

| Setting | Default | Description |
|---------|---------|-------------|
| Show Search | Yes | Display search bar on browse |
| Search Mode | Hybrid | AJAX + client-side filtering |

## Display Options

### Counts Display

| Setting | Effect |
|---------|--------|
| Show on Chips | Number appears on filter buttons |
| Show on Cards | Number appears on taxonomy cards |

### Empty Terms

| Setting | Default | Description |
|---------|---------|-------------|
| Hide Empty | Yes | Don't show terms with no items |

## Slider Settings

### Items Visible

| Setting | Default | Description |
|---------|---------|-------------|
| Slider Items | 5 | Items visible in sliders |
| Mobile Items | 2 | Items visible on mobile |

### Navigation

| Setting | Default | Description |
|---------|---------|-------------|
| Show Arrows | Yes | Show prev/next arrows |
| Show on Hover | Yes | Only show on hover |

## CSS Customization

### Filter Chips

```css
/* Chip container */
.mindful-media-filter-chips {
    display: flex;
    gap: 8px;
    overflow-x: auto;
}

/* Individual chip */
.mindful-media-filter-chip {
    padding: 8px 16px;
    border-radius: 20px;
    background: #f2f2f2;
}

/* Active chip */
.mindful-media-filter-chip.active {
    background: var(--mindful-media-primary);
    color: white;
}
```

### Browse Sections

```css
/* Section container */
.mindful-media-browse-section {
    margin-bottom: 40px;
}

/* Section header */
.mindful-media-section-header {
    font-size: 1.5rem;
    margin-bottom: 16px;
}
```

## Best Practices

### Archive Configuration

- Keep items per page reasonable (12-24)
- Enable filters for large libraries
- Show counts to help users browse

### Browse Configuration

- Enable relevant sections only
- Keep navigation simple
- Match URLs to your site structure

### Mobile Considerations

- Test slider behavior on mobile
- Ensure filters are touch-friendly
- Reduce items per row on small screens
