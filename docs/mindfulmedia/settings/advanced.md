# Advanced Settings

Configure API keys, data management, and advanced options.

## Accessing Settings

Go to **MindfulMedia → Settings → Advanced**

## API Keys

### YouTube Data API

| Setting | Description |
|---------|-------------|
| YouTube API Key | Google API key for YouTube features |

**Required for:**

- Automatic video duration fetching
- Video metadata retrieval

### Getting a YouTube API Key

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project (or select existing)
3. Enable "YouTube Data API v3"
4. Create credentials → API Key
5. Copy the key to settings

**Note:** Vimeo and SoundCloud don't require API keys.

## Data Management

### Uninstall Behavior

| Setting | Effect |
|---------|--------|
| Keep engagement data | Preserve likes, comments, subscriptions, history on uninstall |
| Delete all data | Remove custom tables and data on uninstall |

**When to keep:**

- Temporary deactivation
- Plugin updates
- Troubleshooting

**When to delete:**

- Permanently removing plugin
- Starting fresh
- Privacy compliance

### What Gets Deleted

If "Delete all data" is chosen:

| Data | Deleted |
|------|---------|
| Likes | Yes |
| Comments | Yes |
| Subscriptions | Yes |
| Watch History | Yes |
| Playback Progress | Yes |
| Custom Tables | Yes |
| Plugin Settings | Yes |
| Media Posts | **No** (standard WordPress content) |
| Taxonomies | **No** (standard WordPress data) |

## Database Tables

Custom tables created by MindfulMedia:

| Table | Purpose |
|-------|---------|
| `wp_mindful_media_likes` | User likes |
| `wp_mindful_media_comments` | Media comments |
| `wp_mindful_media_subscriptions` | User subscriptions |
| `wp_mindful_media_watch_history` | View tracking |
| `wp_mindful_media_playback_progress` | Resume positions |

### Table Structure

**Likes:**
```sql
id BIGINT PRIMARY KEY
user_id BIGINT
post_id BIGINT
created_at DATETIME
```

**Subscriptions:**
```sql
id BIGINT PRIMARY KEY
user_id BIGINT
term_id BIGINT
taxonomy VARCHAR(50)
notify TINYINT (0/1)
created_at DATETIME
```

**Watch History:**
```sql
id BIGINT PRIMARY KEY
user_id BIGINT
post_id BIGINT
watched_at DATETIME
duration INT
```

**Playback Progress:**
```sql
id BIGINT PRIMARY KEY
user_id BIGINT
post_id BIGINT
progress FLOAT
updated_at DATETIME
```

## Caching

### Transients Used

| Transient | Purpose | TTL |
|-----------|---------|-----|
| `mm_term_media_count_{id}` | Term item counts | 1 hour |
| `mm_featured_items` | Featured items cache | 30 min |

### Clearing Cache

Plugin caches clear automatically when:

- Content is published
- Content is updated
- Terms are modified

### Manual Clear

Delete transients via:

- Database direct
- Transient manager plugin
- Code: `delete_transient('transient_name')`

## Debug Mode

For troubleshooting (not exposed in UI):

```php
// Add to wp-config.php
define('MINDFUL_MEDIA_DEBUG', true);
```

Enables:

- Verbose error logging
- SQL query logging
- AJAX response debugging

## Import/Export

### Exporting Settings

Settings stored in `wp_options`:

| Option | Content |
|--------|---------|
| `mindful_media_settings` | All plugin settings |

### Backup

Use standard WordPress backup tools:

- Plugin settings via export
- Media posts via WordPress export
- Database backup for engagement data

### Migration

To migrate to new site:

1. Export WordPress content (includes media posts)
2. Export plugin settings
3. Backup custom tables
4. Import on new site
5. Restore settings and tables

## Performance

### Optimization Tips

| Area | Recommendation |
|------|----------------|
| Images | Use optimized thumbnails |
| Queries | Limit items per page |
| Caching | Enable page caching |
| CDN | Serve media from CDN |

### Database Indexes

Custom tables include indexes on:

- `user_id`
- `post_id`
- `term_id`
- `created_at`

## Security

### Nonce Verification

All AJAX requests use WordPress nonces:

```php
// Verified in handlers
wp_verify_nonce($_POST['nonce'], 'mindful_media_nonce')
```

### Capability Checks

| Action | Required Capability |
|--------|-------------------|
| Edit Media | `edit_posts` |
| Delete Media | `delete_posts` |
| Manage Settings | `manage_options` |
| User Engagement | `read` (logged in) |

### Data Sanitization

All inputs sanitized:

- `sanitize_text_field()` for text
- `esc_url_raw()` for URLs
- `intval()` for integers
- `wp_kses_post()` for rich content

## Troubleshooting

### Common Issues

**Duration not fetching:**

1. Check API key is set (YouTube)
2. Verify video URL format
3. Check API quota limits

**Engagement not saving:**

1. Verify tables exist in database
2. Check user is logged in
3. Check AJAX endpoints responding

**Settings not saving:**

1. Check user has `manage_options` capability
2. Verify nonce is valid
3. Check for PHP errors

### Debug Information

Get debug info for support:

1. WordPress version
2. PHP version
3. Plugin version
4. Active theme
5. Conflicting plugins
6. Browser console errors
