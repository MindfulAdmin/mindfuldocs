# Filters

MindfulMedia provides filter hooks to modify plugin behavior and output.

## Overview

Filter hooks allow you to:

- Modify data before it's used
- Customize HTML output
- Change query parameters
- Override default behavior

## Query Filters

### `mindful_media_archive_query_args`

Modify WP_Query arguments for archive listings.

```php
add_filter('mindful_media_archive_query_args', function($query_args, $atts) {
    // Only show featured items
    $query_args['meta_query'][] = array(
        'key' => '_mindful_media_featured',
        'value' => '1'
    );
    return $query_args;
}, 10, 2);
```

**Parameters:**

- `$query_args` (array) - WP_Query arguments
- `$atts` (array) - Shortcode attributes

**Returns:** Modified query arguments array

---

### `mindful_media_browse_query_args`

Modify query for browse page sections.

```php
add_filter('mindful_media_browse_query_args', function($query_args, $section, $term_id) {
    // Limit to 5 items per section
    $query_args['posts_per_page'] = 5;
    return $query_args;
}, 10, 3);
```

**Parameters:**

- `$query_args` (array) - WP_Query arguments
- `$section` (string) - Section name (teachers, topics, etc.)
- `$term_id` (int) - Term ID being queried

---

### `mindful_media_related_query_args`

Modify query for related content.

```php
add_filter('mindful_media_related_query_args', function($query_args, $post_id) {
    // Exclude specific categories from related
    $query_args['tax_query'][] = array(
        'taxonomy' => 'media_category',
        'field' => 'slug',
        'terms' => 'private',
        'operator' => 'NOT IN'
    );
    return $query_args;
}, 10, 2);
```

---

## Output Filters

### `mindful_media_card_html`

Modify individual media card HTML.

```php
add_filter('mindful_media_card_html', function($html, $post_id, $atts) {
    // Add custom data attribute
    $html = str_replace(
        'class="mindful-media-card"',
        'class="mindful-media-card" data-tracking="' . $post_id . '"',
        $html
    );
    return $html;
}, 10, 3);
```

**Parameters:**

- `$html` (string) - Card HTML
- `$post_id` (int) - Media post ID
- `$atts` (array) - Shortcode attributes

---

### `mindful_media_player_html`

Modify media player HTML.

```php
add_filter('mindful_media_player_html', function($html, $url, $source, $atts) {
    // Wrap player in custom container
    return '<div class="my-player-wrapper">' . $html . '</div>';
}, 10, 4);
```

**Parameters:**

- `$html` (string) - Player HTML
- `$url` (string) - Media URL
- `$source` (string) - Source type (youtube, vimeo, etc.)
- `$atts` (array) - Player attributes

---

### `mindful_media_thumbnail_html`

Modify thumbnail HTML.

```php
add_filter('mindful_media_thumbnail_html', function($html, $post_id, $size) {
    // Add lazy loading
    return str_replace('<img', '<img loading="lazy"', $html);
}, 10, 3);
```

---

### `mindful_media_duration_display`

Modify how duration is displayed.

```php
add_filter('mindful_media_duration_display', function($display, $hours, $minutes) {
    // Custom format
    if ($hours > 0) {
        return $hours . 'h ' . $minutes . 'm';
    }
    return $minutes . ' min';
}, 10, 3);
```

---

## Data Filters

### `mindful_media_card_data`

Modify card data before rendering.

```php
add_filter('mindful_media_card_data', function($data, $post_id) {
    // Add custom field to card data
    $data['custom_field'] = get_post_meta($post_id, '_custom_field', true);
    return $data;
}, 10, 2);
```

**Default data structure:**

```php
array(
    'id' => $post_id,
    'title' => $title,
    'thumbnail' => $thumbnail_url,
    'duration' => $duration,
    'teacher' => $teacher_name,
    'url' => $permalink,
    'type' => $media_type
)
```

---

### `mindful_media_settings`

Modify settings before use.

```php
add_filter('mindful_media_settings', function($settings) {
    // Force specific setting
    $settings['items_per_page'] = 24;
    return $settings;
});
```

---

## Email Filters

### `mindful_media_notification_subject`

Modify notification email subject.

```php
add_filter('mindful_media_notification_subject', function($subject, $post, $term) {
    return '🎬 ' . $subject; // Add emoji
}, 10, 3);
```

---

### `mindful_media_notification_body`

Modify notification email body.

```php
add_filter('mindful_media_notification_body', function($body, $post, $term, $user) {
    // Add custom footer
    $body .= '<p>Thanks for being a valued member!</p>';
    return $body;
}, 10, 4);
```

---

### `mindful_media_notification_recipients`

Modify who receives notifications.

```php
add_filter('mindful_media_notification_recipients', function($user_ids, $term_id, $taxonomy) {
    // Exclude certain users
    return array_filter($user_ids, function($id) {
        return !user_has_opted_out($id);
    });
}, 10, 3);
```

---

## Access Control Filters

### `mindful_media_user_can_view`

Override access control checks.

```php
add_filter('mindful_media_user_can_view', function($can_view, $post_id, $user_id) {
    // Custom access logic
    if (user_is_vip($user_id)) {
        return true; // VIPs see everything
    }
    return $can_view;
}, 10, 3);
```

---

### `mindful_media_locked_message`

Modify locked content message.

```php
add_filter('mindful_media_locked_message', function($message, $post_id, $required_levels) {
    // Custom message based on required level
    $level_name = get_the_title($required_levels[0]);
    return "Upgrade to {$level_name} to access this content!";
}, 10, 3);
```

---

## CSS/JS Filters

### `mindful_media_frontend_styles`

Add or modify frontend styles.

```php
add_filter('mindful_media_frontend_styles', function($styles) {
    $styles['my-custom'] = array(
        'src' => plugin_dir_url(__FILE__) . 'custom.css',
        'deps' => array('mindful-media-frontend'),
        'ver' => '1.0.0'
    );
    return $styles;
});
```

---

### `mindful_media_frontend_scripts`

Add or modify frontend scripts.

```php
add_filter('mindful_media_frontend_scripts', function($scripts) {
    $scripts['my-custom'] = array(
        'src' => plugin_dir_url(__FILE__) . 'custom.js',
        'deps' => array('mindful-media-frontend', 'jquery'),
        'ver' => '1.0.0',
        'in_footer' => true
    );
    return $scripts;
});
```

---

## Usage Examples

### Exclude Categories from Archive

```php
add_filter('mindful_media_archive_query_args', function($args, $atts) {
    // Exclude "draft" and "internal" categories
    $args['tax_query'][] = array(
        'taxonomy' => 'media_category',
        'field' => 'slug',
        'terms' => array('draft', 'internal'),
        'operator' => 'NOT IN'
    );
    return $args;
}, 10, 2);
```

### Custom Card Layout

```php
add_filter('mindful_media_card_html', function($html, $post_id) {
    // Add view count badge
    $views = get_post_meta($post_id, '_view_count', true) ?: 0;
    $badge = '<span class="view-badge">' . $views . ' views</span>';
    
    // Insert before closing card div
    return str_replace('</div><!-- .mindful-media-card -->', 
        $badge . '</div><!-- .mindful-media-card -->', $html);
}, 10, 2);
```

### Premium-Only Content Filter

```php
add_filter('mindful_media_archive_query_args', function($args) {
    // Only show free content to non-members
    if (!current_user_can('premium_member')) {
        $args['meta_query'][] = array(
            'key' => '_premium_only',
            'compare' => 'NOT EXISTS'
        );
    }
    return $args;
});
```
