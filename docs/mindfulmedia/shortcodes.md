# Shortcodes Reference

MindfulMedia provides 6 shortcodes for displaying media content anywhere on your site.

## Overview

| Shortcode | Purpose |
|-----------|---------|
| `[mindful_media_browse]` | Full browse page with navigation tabs |
| `[mindful_media_archive]` | Grid of media items with filters |
| `[mindful_media]` | Single media embed or playlist |
| `[mindful_media_row]` | Horizontal category slider |
| `[mindful_media_taxonomy_archive]` | Full taxonomy archive page |
| `[mindful_media_library]` | User's personal library |

---

## `[mindful_media_browse]`

Creates a full browse experience with navigation tabs and category sections.

### Attributes

| Attribute | Default | Description |
|-----------|---------|-------------|
| `show_featured` | `true` | Show featured hero section |
| `show_nav` | `true` | Show category navigation tabs |
| `sections` | `teachers,topics,playlists,types` | Comma-separated sections to display |

### Examples

```html
<!-- Full browse page -->
[mindful_media_browse]

<!-- Without featured section -->
[mindful_media_browse show_featured="false"]

<!-- Only show teachers and topics -->
[mindful_media_browse sections="teachers,topics"]
```

### Tab Behavior

The browse page has two display modes:

**HOME Tab:**

- Shows taxonomy cards in horizontal sliders
- Click a card to view that taxonomy's archive
- Discovery-focused view

**Individual Tabs (Teachers, Topics, etc.):**

- Shows Netflix-style video rows for each term
- Each teacher/topic gets its own row with their videos
- Click a video to open the modal player

---

## `[mindful_media_archive]`

Displays a YouTube-style grid of media items with filter chips.

### Attributes

| Attribute | Default | Description |
|-----------|---------|-------------|
| `per_page` | `12` | Items per page |
| `show_filters` | `true` | Show horizontal filter chips |
| `show_pagination` | `true` | Show pagination |
| `category` | `''` | Filter by category slug |
| `type` | `''` | Filter by media type (`audio` or `video`) |
| `topic` | `''` | Filter by topic slug |
| `teacher` | `''` | Filter by teacher slug |
| `featured` | `''` | Set to `true` for featured items only |

### Examples

```html
<!-- Basic archive -->
[mindful_media_archive]

<!-- 20 items per page, no filters -->
[mindful_media_archive per_page="20" show_filters="false"]

<!-- Only meditation videos -->
[mindful_media_archive topic="meditation" type="video"]

<!-- Featured items only -->
[mindful_media_archive featured="true" per_page="6"]

<!-- Specific teacher's content -->
[mindful_media_archive teacher="john-smith"]
```

---

## `[mindful_media]`

Embeds a single media item or playlist with a clickable thumbnail that opens the modal player.

### Attributes

| Attribute | Default | Description |
|-----------|---------|-------------|
| `id` | `''` | Media item post ID |
| `playlist` | `''` | Playlist slug (alternative to id) |
| `show_thumbnail` | `true` | Show clickable thumbnail |
| `autoplay` | `false` | Auto-play when modal opens |
| `size` | `medium` | Embed size (see options below) |

### Size Options

| Value | Width |
|-------|-------|
| `small` | 320px |
| `medium` | 560px |
| `large` | 800px |
| `full` | 100% |
| Custom | Any px/% value (e.g., `640px`, `75%`) |

### Examples

```html
<!-- Single media by ID -->
[mindful_media id="123"]

<!-- Playlist embed -->
[mindful_media playlist="beginner-course"]

<!-- Large size with autoplay -->
[mindful_media id="123" size="large" autoplay="true"]

<!-- Full width -->
[mindful_media id="123" size="full"]

<!-- Custom size -->
[mindful_media id="123" size="640px"]
```

---

## `[mindful_media_row]`

Displays a Netflix-style horizontal slider of items from a taxonomy.

### Attributes

| Attribute | Default | Description |
|-----------|---------|-------------|
| `taxonomy` | `media_teacher` | Taxonomy to display |
| `title` | `''` | Custom section title |
| `limit` | `12` | Maximum items shown |
| `show_link` | `true` | Show "View All" link |

### Taxonomy Options

| Value | Description |
|-------|-------------|
| `media_teacher` | Teachers |
| `media_topic` | Topics |
| `media_category` | Categories |
| `media_series` | Playlists |

### Examples

```html
<!-- Browse by topic -->
[mindful_media_row taxonomy="media_topic" title="Browse by Topic"]

<!-- Teachers without "View All" link -->
[mindful_media_row taxonomy="media_teacher" show_link="false"]

<!-- Playlists with custom title -->
[mindful_media_row taxonomy="media_series" title="Featured Courses"]

<!-- Categories, limited to 6 -->
[mindful_media_row taxonomy="media_category" limit="6"]
```

---

## `[mindful_media_taxonomy_archive]`

Displays a full page of all terms from a taxonomy, each as a Netflix-style row with their media items.

### Attributes

| Attribute | Default | Description |
|-----------|---------|-------------|
| `taxonomy` | `media_teacher` | Taxonomy to display |
| `title` | `''` | Custom page title |
| `items_per_row` | `10` | Items per row |
| `orderby` | `name` | Term order (`name`, `count`, `slug`) |
| `order` | `ASC` | Sort direction (`ASC`, `DESC`) |
| `hide_empty` | `true` | Hide terms with no items |

### Examples

```html
<!-- All playlists -->
[mindful_media_taxonomy_archive taxonomy="media_series" title="All Courses"]

<!-- All teachers, ordered by content count -->
[mindful_media_taxonomy_archive taxonomy="media_teacher" orderby="count" order="DESC"]

<!-- Topics with more items per row -->
[mindful_media_taxonomy_archive taxonomy="media_topic" items_per_row="15"]
```

!!! note "Password Protection"
    When displaying playlists (`media_series`), password-protected playlists show a lock icon and require password entry before revealing content.

---

## `[mindful_media_library]`

Displays the user's personal library with their engagement history.

### Attributes

This shortcode has no attributes.

### Example

```html
[mindful_media_library]
```

### Sections Displayed

| Section | Description |
|---------|-------------|
| **Continue Watching** | Videos with saved progress (< 90% complete) |
| **Liked Videos** | Videos the user has liked |
| **Watch History** | Recently viewed videos |
| **Subscriptions** | Followed teachers, topics, playlists |

!!! warning "Login Required"
    This shortcode requires the user to be logged in. Guests see a login prompt.

!!! info "Auto-Created Page"
    A "My Library" page with this shortcode is automatically created when the plugin is activated.

---

## Common Patterns

### Landing Page

```html
<!-- Hero section with featured playlist -->
[mindful_media playlist="featured-course" size="full"]

<!-- Full browse experience -->
[mindful_media_browse]
```

### Category Page

```html
<!-- All meditation content -->
[mindful_media_archive topic="meditation" per_page="24"]
```

### Teacher Profile

```html
<!-- Teacher's content grid -->
[mindful_media_archive teacher="john-smith" per_page="12"]
```

### Course Page

```html
<!-- Course playlist embed -->
[mindful_media playlist="complete-course" size="large"]
```

### Homepage Sections

```html
<!-- Featured topics -->
[mindful_media_row taxonomy="media_topic" title="Explore Topics" limit="8"]

<!-- Latest from teachers -->
[mindful_media_row taxonomy="media_teacher" title="Our Teachers" limit="6"]

<!-- Featured playlists -->
[mindful_media_row taxonomy="media_series" title="Popular Courses" limit="4"]
```
