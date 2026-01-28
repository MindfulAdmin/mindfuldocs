# Database Schema

MindfulMedia uses custom database tables for engagement features.

## Overview

The plugin creates 5 custom tables on activation:

| Table | Purpose |
|-------|---------|
| `wp_mindful_media_likes` | User likes |
| `wp_mindful_media_comments` | Media comments |
| `wp_mindful_media_subscriptions` | User subscriptions |
| `wp_mindful_media_watch_history` | View tracking |
| `wp_mindful_media_playback_progress` | Resume positions |

## Table Structures

### Likes Table

```sql
CREATE TABLE wp_mindful_media_likes (
    id BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
    user_id BIGINT(20) UNSIGNED NOT NULL,
    post_id BIGINT(20) UNSIGNED NOT NULL,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (id),
    UNIQUE KEY user_post (user_id, post_id),
    KEY post_id (post_id),
    KEY user_id (user_id)
);
```

**Columns:**

| Column | Type | Description |
|--------|------|-------------|
| `id` | BIGINT | Primary key |
| `user_id` | BIGINT | WordPress user ID |
| `post_id` | BIGINT | Media post ID |
| `created_at` | DATETIME | When the like was added |

**Indexes:**

- Primary key on `id`
- Unique constraint on `user_id + post_id` (prevents duplicate likes)
- Index on `post_id` (for counting likes per post)
- Index on `user_id` (for user's liked items)

---

### Comments Table

```sql
CREATE TABLE wp_mindful_media_comments (
    id BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
    user_id BIGINT(20) UNSIGNED NOT NULL,
    post_id BIGINT(20) UNSIGNED NOT NULL,
    parent_id BIGINT(20) UNSIGNED DEFAULT 0,
    content TEXT NOT NULL,
    status VARCHAR(20) DEFAULT 'pending',
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (id),
    KEY post_id (post_id),
    KEY user_id (user_id),
    KEY parent_id (parent_id),
    KEY status (status)
);
```

**Columns:**

| Column | Type | Description |
|--------|------|-------------|
| `id` | BIGINT | Primary key |
| `user_id` | BIGINT | Author user ID |
| `post_id` | BIGINT | Media post ID |
| `parent_id` | BIGINT | Parent comment (for threading) |
| `content` | TEXT | Comment text |
| `status` | VARCHAR(20) | pending, approved, spam, trash |
| `created_at` | DATETIME | Timestamp |

---

### Subscriptions Table

```sql
CREATE TABLE wp_mindful_media_subscriptions (
    id BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
    user_id BIGINT(20) UNSIGNED NOT NULL,
    term_id BIGINT(20) UNSIGNED NOT NULL,
    taxonomy VARCHAR(50) NOT NULL,
    notify TINYINT(1) DEFAULT 1,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (id),
    UNIQUE KEY user_term (user_id, term_id, taxonomy),
    KEY user_id (user_id),
    KEY term_id (term_id),
    KEY taxonomy (taxonomy)
);
```

**Columns:**

| Column | Type | Description |
|--------|------|-------------|
| `id` | BIGINT | Primary key |
| `user_id` | BIGINT | Subscriber user ID |
| `term_id` | BIGINT | Term ID (teacher, topic, etc.) |
| `taxonomy` | VARCHAR(50) | Taxonomy name |
| `notify` | TINYINT | Email notifications enabled |
| `created_at` | DATETIME | Subscription date |

**Taxonomy Values:**

- `media_teacher`
- `media_topic`
- `media_category`
- `media_series`

---

### Watch History Table

```sql
CREATE TABLE wp_mindful_media_watch_history (
    id BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
    user_id BIGINT(20) UNSIGNED NOT NULL,
    post_id BIGINT(20) UNSIGNED NOT NULL,
    watched_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    duration INT DEFAULT 0,
    PRIMARY KEY (id),
    KEY user_id (user_id),
    KEY post_id (post_id),
    KEY watched_at (watched_at)
);
```

**Columns:**

| Column | Type | Description |
|--------|------|-------------|
| `id` | BIGINT | Primary key |
| `user_id` | BIGINT | Viewer user ID |
| `post_id` | BIGINT | Media post ID |
| `watched_at` | DATETIME | View timestamp |
| `duration` | INT | Seconds watched |

**Note:** Multiple entries per user/post allowed (tracks each view).

---

### Playback Progress Table

```sql
CREATE TABLE wp_mindful_media_playback_progress (
    id BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
    user_id BIGINT(20) UNSIGNED NOT NULL,
    post_id BIGINT(20) UNSIGNED NOT NULL,
    progress FLOAT DEFAULT 0,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    PRIMARY KEY (id),
    UNIQUE KEY user_post (user_id, post_id),
    KEY user_id (user_id),
    KEY progress (progress)
);
```

**Columns:**

| Column | Type | Description |
|--------|------|-------------|
| `id` | BIGINT | Primary key |
| `user_id` | BIGINT | User ID |
| `post_id` | BIGINT | Media post ID |
| `progress` | FLOAT | Percentage complete (0-100) |
| `updated_at` | DATETIME | Last update time |

**Progress Logic:**

- `0` = Not started
- `1-89` = In progress (Continue Watching)
- `90-100` = Completed

---

## Querying Data

### Get User's Likes

```php
global $wpdb;
$table = $wpdb->prefix . 'mindful_media_likes';

$liked_posts = $wpdb->get_col($wpdb->prepare(
    "SELECT post_id FROM {$table} WHERE user_id = %d ORDER BY created_at DESC",
    $user_id
));
```

### Get Like Count

```php
$count = $wpdb->get_var($wpdb->prepare(
    "SELECT COUNT(*) FROM {$table} WHERE post_id = %d",
    $post_id
));
```

### Check If User Liked

```php
$liked = $wpdb->get_var($wpdb->prepare(
    "SELECT id FROM {$table} WHERE user_id = %d AND post_id = %d",
    $user_id, $post_id
));
$is_liked = !empty($liked);
```

### Get User's Subscriptions

```php
$table = $wpdb->prefix . 'mindful_media_subscriptions';

$subscriptions = $wpdb->get_results($wpdb->prepare(
    "SELECT term_id, taxonomy, notify FROM {$table} WHERE user_id = %d",
    $user_id
));
```

### Get Subscribers for Term

```php
$subscribers = $wpdb->get_col($wpdb->prepare(
    "SELECT user_id FROM {$table} 
     WHERE term_id = %d AND taxonomy = %s AND notify = 1",
    $term_id, $taxonomy
));
```

### Get Continue Watching

```php
$table = $wpdb->prefix . 'mindful_media_playback_progress';

$in_progress = $wpdb->get_results($wpdb->prepare(
    "SELECT post_id, progress FROM {$table} 
     WHERE user_id = %d AND progress > 0 AND progress < 90 
     ORDER BY updated_at DESC",
    $user_id
));
```

### Get Watch History

```php
$table = $wpdb->prefix . 'mindful_media_watch_history';

$history = $wpdb->get_results($wpdb->prepare(
    "SELECT post_id, watched_at FROM {$table} 
     WHERE user_id = %d 
     ORDER BY watched_at DESC 
     LIMIT 50",
    $user_id
));
```

---

## Data Management

### Table Creation

Tables are created on plugin activation via `dbDelta()`:

```php
require_once(ABSPATH . 'wp-admin/includes/upgrade.php');
dbDelta($sql);
```

### Table Deletion

On uninstall (if "Delete data" option set):

```php
$wpdb->query("DROP TABLE IF EXISTS {$wpdb->prefix}mindful_media_likes");
// ... repeat for each table
```

### Data Export

Export user data for GDPR:

```php
function export_user_engagement_data($user_id) {
    global $wpdb;
    
    $data = array(
        'likes' => $wpdb->get_results($wpdb->prepare(
            "SELECT * FROM {$wpdb->prefix}mindful_media_likes WHERE user_id = %d",
            $user_id
        )),
        'comments' => $wpdb->get_results($wpdb->prepare(
            "SELECT * FROM {$wpdb->prefix}mindful_media_comments WHERE user_id = %d",
            $user_id
        )),
        'subscriptions' => $wpdb->get_results($wpdb->prepare(
            "SELECT * FROM {$wpdb->prefix}mindful_media_subscriptions WHERE user_id = %d",
            $user_id
        )),
        'history' => $wpdb->get_results($wpdb->prepare(
            "SELECT * FROM {$wpdb->prefix}mindful_media_watch_history WHERE user_id = %d",
            $user_id
        )),
        'progress' => $wpdb->get_results($wpdb->prepare(
            "SELECT * FROM {$wpdb->prefix}mindful_media_playback_progress WHERE user_id = %d",
            $user_id
        ))
    );
    
    return $data;
}
```

---

## Performance

### Indexes

All tables have indexes on commonly queried columns:

- `user_id` - For user-specific queries
- `post_id` - For post-specific aggregations
- `term_id` - For subscription lookups
- Composite indexes where appropriate

### Query Optimization

- Use prepared statements
- Limit results when possible
- Cache frequently accessed data
- Use transients for counts

### Cleanup

Consider periodic cleanup of old data:

```php
// Delete watch history older than 1 year
$wpdb->query($wpdb->prepare(
    "DELETE FROM {$wpdb->prefix}mindful_media_watch_history 
     WHERE watched_at < %s",
    date('Y-m-d', strtotime('-1 year'))
));
```
