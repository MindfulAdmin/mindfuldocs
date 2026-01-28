# Email Settings

Configure email notifications sent to subscribers.

## Accessing Settings

Go to **MindfulMedia → Settings → Emails**

## Sender Settings

### From Information

| Setting | Description |
|---------|-------------|
| From Name | Name shown in recipient's inbox |
| From Email | Reply-to email address |

**Recommendations:**

```
From Name: "Mindful Design"
From Email: "notifications@yoursite.com"
```

### Notification Schedule

| Option | Behavior |
|--------|----------|
| Instant | Send immediately on publish |
| Hourly Digest | Batch notifications every hour |
| Daily Digest | Batch notifications once per day |

## Email Template

### Header

| Setting | Description |
|---------|-------------|
| Header Logo | Upload logo image (optional) |
| Header Text | Text shown if no logo |
| Header Background | Background color (#hex) |
| Header Text Color | Text color (#hex) |

**Logo Tips:**

- Use PNG with transparency
- Keep height under 60px
- Use HTTPS URL

### Body Template

Customize the email body content using placeholders:

**Available Placeholders:**

| Placeholder | Replaced With |
|-------------|---------------|
| `{user_name}` | Recipient's display name |
| `{post_title}` | Media item title |
| `{post_excerpt}` | Media item description |
| `{post_url}` | Link to the content |
| `{term_name}` | Teacher/topic/playlist name |
| `{site_name}` | Your website name |
| `{thumbnail_url}` | Featured image URL |
| `{button_color}` | CTA button background |
| `{button_text_color}` | CTA button text |

**Default Template:**

```html
Hi {user_name},

New content is available from <strong>{term_name}</strong>:

<div style="background: #f5f5f5; padding: 15px; border-radius: 6px; margin: 20px 0;">
<strong>{post_title}</strong>
<p style="margin: 8px 0 0; color: #666;">{post_excerpt}</p>
</div>

<a href="{post_url}" style="display: inline-block; background: {button_color}; color: {button_text_color}; padding: 12px 24px; border-radius: 4px; text-decoration: none; font-weight: 600;">Watch Now</a>
```

### Footer

| Setting | Description |
|---------|-------------|
| Footer Text | Text below main content |

**Default:**
```
You received this email because you subscribed to updates.
Click unsubscribe to stop receiving these emails.
```

**Note:** HTML is supported in footer text.

### Colors

| Setting | Default | Description |
|---------|---------|-------------|
| Button Background | `#DAA520` | CTA button color |
| Button Text | `#ffffff` | CTA button text color |

## Email Preview

The settings page includes a live preview:

- Updates as you change settings
- Shows header with logo/text
- Shows body with placeholder examples
- Shows footer text
- Reflects color choices

## Test Email

### Sending a Test

1. Scroll to **Email Preview & Test**
2. Enter your email address
3. Click **Send Test Email**

### What to Check

- Email arrives in inbox (not spam)
- Header displays correctly
- Logo appears (if set)
- Colors match settings
- Links work
- Mobile rendering

### Troubleshooting

**"Email sent" but nothing received:**

1. Check spam folder
2. Verify SMTP is configured
3. Check WP Mail SMTP logs
4. Test with a different email address

**"Email failed":**

- Check error message displayed
- Verify From Email is valid
- Configure WP Mail SMTP properly

## WP Mail SMTP Setup

For reliable email delivery:

1. Install **WP Mail SMTP** plugin
2. Configure a mailer:
    - SendGrid
    - Mailgun
    - Amazon SES
    - Gmail (low volume only)
3. Verify domain authentication (SPF, DKIM)
4. Test with WP Mail SMTP's test feature

## Email Types

### Instant Notification

Sent immediately when content is published:

```
Subject: New from [Teacher Name]: [Video Title]
Body: Your template with placeholders replaced
```

### Digest Emails

Combines multiple notifications:

```
Subject: Your Daily Update from [Site Name]
Body: List of all new content since last digest
```

## Best Practices

### Subject Lines

Keep subjects:

- Under 50 characters
- Clear and descriptive
- Including content title

### Content

- Single clear CTA ("Watch Now")
- Brief description
- Mobile-friendly formatting

### Deliverability

- Use authenticated sending domain
- Monitor bounce rates
- Keep subscriber list clean
- Include unsubscribe option (automatic)

### Testing

- Test all template changes
- Check on multiple email clients
- Verify mobile rendering
- Test with different email providers
