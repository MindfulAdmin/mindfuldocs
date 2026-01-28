# Hooks & Actions

MindfulMedia provides action hooks for developers to extend functionality.

## Overview

Action hooks allow you to:

- Execute code at specific points
- Add custom functionality
- Integrate with other plugins

## Available Actions

### Content Actions

#### `mindful_media_before_archive`

Fires before the archive grid renders.

```php
add_action('mindful_media_before_archive', function($atts) {
    echo '<div class="my-custom-header">Custom Header</div>';
}, 10, 1);
```

**Parameters:**

- `$atts` (array) - Shortcode attributes

---

#### `mindful_media_after_archive`

Fires after the archive grid renders.

```php
add_action('mindful_media_after_archive', function($atts) {
    echo '<div class="my-custom-footer">Custom Footer</div>';
}, 10, 1);
```

---

#### `mindful_media_before_card`

Fires before each media card renders.

```php
add_action('mindful_media_before_card', function($post_id) {
    // Add custom markup before card
}, 10, 1);
```

**Parameters:**

- `$post_id` (int) - The media post ID

---

#### `mindful_media_after_card`

Fires after each media card renders.

```php
add_action('mindful_media_after_card', function($post_id) {
    // Add custom markup after card
}, 10, 1);
```

---

### Player Actions

#### `mindful_media_before_player`

Fires before the player renders.

```php
add_action('mindful_media_before_player', function($post_id, $url, $source) {
    // Add pre-player content
}, 10, 3);
```

**Parameters:**

- `$post_id` (int) - Media post ID
- `$url` (string) - Media URL
- `$source` (string) - Source type (youtube, vimeo, etc.)

---

#### `mindful_media_after_player`

Fires after the player renders.

```php
add_action('mindful_media_after_player', function($post_id, $url, $source) {
    // Add post-player content
}, 10, 3);
```

---

### Engagement Actions

#### `mindful_media_user_liked`

Fires when a user likes a media item.

```php
add_action('mindful_media_user_liked', function($user_id, $post_id) {
    // Track analytics
    // Send notification
}, 10, 2);
```

**Parameters:**

- `$user_id` (int) - User who liked
- `$post_id` (int) - Media item liked

---

#### `mindful_media_user_unliked`

Fires when a user unlikes a media item.

```php
add_action('mindful_media_user_unliked', function($user_id, $post_id) {
    // Update analytics
}, 10, 2);
```

---

#### `mindful_media_user_subscribed`

Fires when a user subscribes to a taxonomy term.

```php
add_action('mindful_media_user_subscribed', function($user_id, $term_id, $taxonomy) {
    // Welcome email
    // Track subscription
}, 10, 3);
```

**Parameters:**

- `$user_id` (int) - User who subscribed
- `$term_id` (int) - Term subscribed to
- `$taxonomy` (string) - Taxonomy type

---

#### `mindful_media_user_unsubscribed`

Fires when a user unsubscribes.

```php
add_action('mindful_media_user_unsubscribed', function($user_id, $term_id, $taxonomy) {
    // Goodbye email (optional)
    // Update analytics
}, 10, 3);
```

---

#### `mindful_media_comment_posted`

Fires when a comment is posted.

```php
add_action('mindful_media_comment_posted', function($comment_id, $post_id, $user_id) {
    // Notify content owner
    // Moderate content
}, 10, 3);
```

---

### Notification Actions

#### `mindful_media_before_notification`

Fires before a notification email is sent.

```php
add_action('mindful_media_before_notification', function($user_id, $post_id, $term_id) {
    // Log notification
    // Check user preferences
}, 10, 3);
```

---

#### `mindful_media_after_notification`

Fires after a notification email is sent.

```php
add_action('mindful_media_after_notification', function($user_id, $post_id, $sent) {
    // Update sent count
    // Log delivery status
}, 10, 3);
```

**Parameters:**

- `$user_id` (int) - Recipient user
- `$post_id` (int) - Media item notified about
- `$sent` (bool) - Whether email was sent successfully

---

### Progress Actions

#### `mindful_media_progress_saved`

Fires when playback progress is saved.

```php
add_action('mindful_media_progress_saved', function($user_id, $post_id, $progress) {
    // Track viewing patterns
    // Award badges at milestones
}, 10, 3);
```

**Parameters:**

- `$user_id` (int) - User
- `$post_id` (int) - Media item
- `$progress` (float) - Progress percentage (0-100)

---

#### `mindful_media_video_completed`

Fires when a video is marked complete (>90%).

```php
add_action('mindful_media_video_completed', function($user_id, $post_id) {
    // Award completion badge
    // Update course progress
    // Unlock next item
}, 10, 2);
```

---

### Admin Actions

#### `mindful_media_settings_saved`

Fires when plugin settings are saved.

```php
add_action('mindful_media_settings_saved', function($settings) {
    // Clear related caches
    // Update dependent systems
}, 10, 1);
```

---

## Usage Examples

### Track Video Views

```php
add_action('mindful_media_progress_saved', function($user_id, $post_id, $progress) {
    // Only count first view (progress > 0 for first time)
    $viewed = get_user_meta($user_id, '_viewed_' . $post_id, true);
    
    if (!$viewed && $progress > 0) {
        update_user_meta($user_id, '_viewed_' . $post_id, time());
        
        // Increment view counter
        $views = get_post_meta($post_id, '_view_count', true) ?: 0;
        update_post_meta($post_id, '_view_count', $views + 1);
    }
}, 10, 3);
```

### Award Badges

```php
add_action('mindful_media_video_completed', function($user_id, $post_id) {
    // Count completed videos
    global $wpdb;
    $completed = $wpdb->get_var($wpdb->prepare(
        "SELECT COUNT(*) FROM {$wpdb->prefix}mindful_media_playback_progress 
         WHERE user_id = %d AND progress >= 90",
        $user_id
    ));
    
    // Award badges at milestones
    if ($completed == 10) {
        award_badge($user_id, 'watched_10_videos');
    } elseif ($completed == 50) {
        award_badge($user_id, 'watched_50_videos');
    }
}, 10, 2);
```

### Custom Analytics

```php
add_action('mindful_media_user_liked', function($user_id, $post_id) {
    // Send to analytics platform
    if (function_exists('gtag')) {
        echo "<script>gtag('event', 'like', {'post_id': {$post_id}});</script>";
    }
}, 10, 2);
```
