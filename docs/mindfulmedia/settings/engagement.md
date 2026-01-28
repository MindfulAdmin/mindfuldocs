# Engagement Settings

Configure user engagement features like likes, comments, and subscriptions.

## Accessing Settings

Go to **MindfulMedia → Settings → Engagement**

## Engagement Features

### Likes

| Setting | Default | Description |
|---------|---------|-------------|
| Enable Likes | Yes | Allow users to like content |

**When enabled:**

- Like button appears on media items
- Like counts visible on cards
- Liked items saved to user's library

### Comments

| Setting | Default | Description |
|---------|---------|-------------|
| Enable Comments | Yes | Allow comments on media |
| Auto-Approve | No | Skip moderation queue |

**When enabled:**

- Comment section appears below player
- Users can post and reply
- Manage comments in WordPress admin

### Subscriptions

| Setting | Default | Description |
|---------|---------|-------------|
| Enable Subscriptions | Yes | Allow following taxonomies |

**When enabled:**

- Subscribe button on taxonomy pages
- Email notifications for new content
- Manage in My Library

## Guest Behavior

### Login Prompts

When guests try to engage:

- "Log in to like this video"
- "Create an account to subscribe"
- Links to login/registration pages

### Login URL

| Setting | Default | Description |
|---------|---------|-------------|
| Login URL | WP Login | Page for login prompts |

Set a custom login page URL if you use a custom login form.

## My Library

### Library Page

| Setting | Default | Description |
|---------|---------|-------------|
| Library Page | Auto-created | Page with library shortcode |

Select or change the My Library page.

### WooCommerce Integration

| Setting | Default | Description |
|---------|---------|-------------|
| WooCommerce Tab | No | Add to My Account page |

**When enabled:**

- New "My Library" tab in WooCommerce My Account
- Same content as standalone library page
- Integrates with existing account area

## Database Tables

Engagement data is stored in custom tables:

| Table | Data |
|-------|------|
| `wp_mindful_media_likes` | User ID, Post ID, Timestamp |
| `wp_mindful_media_comments` | Comment data, User, Post |
| `wp_mindful_media_subscriptions` | User ID, Term ID, Type |
| `wp_mindful_media_watch_history` | User ID, Post ID, View time |
| `wp_mindful_media_playback_progress` | User ID, Post ID, Progress |

## Visibility

### Engagement UI Location

Engagement elements appear on:

| Location | What Shows |
|----------|------------|
| Single Media Page | Like, Subscribe, Comments |
| Modal Player | Like, Subscribe, Comments |
| Media Cards | Like count (optional) |
| My Library | All engagement data |

### Conditional Display

| User State | What They See |
|------------|---------------|
| Logged In | Full engagement UI |
| Guest | Login prompts |
| Admin | All + moderation options |

## Styling

### Like Button

```css
/* Like button container */
.mm-like-btn {
    display: flex;
    align-items: center;
    gap: 6px;
    cursor: pointer;
}

/* Heart icon */
.mm-like-btn svg {
    width: 24px;
    height: 24px;
    fill: transparent;
    stroke: currentColor;
}

/* Liked state */
.mm-like-btn.liked svg {
    fill: #ff0000;
    stroke: #ff0000;
}

/* Like count */
.mm-like-count {
    font-size: 14px;
}
```

### Subscribe Button

```css
/* Subscribe button */
.mm-subscribe-btn {
    padding: 8px 16px;
    border-radius: 20px;
    background: var(--mindful-media-secondary);
    color: white;
}

/* Subscribed state */
.mm-subscribe-btn.subscribed {
    background: #666;
}
```

### Comments Section

```css
/* Comments container */
.mm-comments-section {
    margin-top: 24px;
    padding-top: 24px;
    border-top: 1px solid #333;
}

/* Individual comment */
.mm-comment {
    display: flex;
    gap: 12px;
    margin-bottom: 16px;
}

/* Comment avatar */
.mm-comment-avatar {
    width: 40px;
    height: 40px;
    border-radius: 50%;
}

/* Comment content */
.mm-comment-content {
    flex: 1;
}

/* Comment form */
.mm-comment-form textarea {
    width: 100%;
    min-height: 80px;
}
```

## Best Practices

### Enable Strategically

- **Likes**: Great for all content types
- **Comments**: Best for community-focused sites
- **Subscriptions**: Essential for regular content publishers

### Moderation

- Auto-approve for trusted communities
- Manual approval for public sites
- Monitor regularly for spam

### User Experience

- Make engagement buttons prominent
- Show clear feedback on actions
- Guide users to create accounts
