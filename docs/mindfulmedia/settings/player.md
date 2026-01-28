# Player Settings

Configure video and audio player behavior.

## Accessing Settings

Go to **MindfulMedia → Settings → Player**

## Playback Settings

### Autoplay

| Setting | Default | Description |
|---------|---------|-------------|
| Autoplay | Off | Auto-start playback when modal opens |

**Note:** Browser policies may block autoplay with sound.

### Related Videos

| Setting | Default | Description |
|---------|---------|-------------|
| Show Related | Yes | Show related videos after playback |

### YouTube Options

| Setting | Default | Description |
|---------|---------|-------------|
| Hide End Screen | Off | Cover YouTube's end-screen recommendations |

When enabled, the plugin covers YouTube's end-screen overlay to prevent users from leaving your site.

## Progress Bar

### Color

| Setting | Default | Description |
|---------|---------|-------------|
| Progress Color | `#ff0000` | Color of the playback progress bar |

This color applies to:

- Video progress bar
- Audio progress bar
- Volume slider fill

### Style

The progress bar uses a gradient fill:

```css
background: linear-gradient(
    to right,
    var(--mindful-media-progress-color) 0%,
    var(--mindful-media-progress-color) 50%, /* current position */
    rgba(255,255,255,0.3) 50%,
    rgba(255,255,255,0.3) 100%
);
```

## Audio Player

### Controls

The audio player includes:

- Play/Pause button
- Progress bar (draggable)
- Current time / Duration
- Volume slider
- Mute button

### Styling

```css
/* Audio controls container */
.mindful-media-audio-controls {
    background: rgba(0, 0, 0, 0.8);
    padding: 10px 15px;
}

/* Volume slider */
.mindful-media-volume-slider input[type="range"] {
    accent-color: var(--mindful-media-progress-color);
}
```

## Modal Player

### Overlay

| Setting | Effect |
|---------|--------|
| Dark overlay | Semi-transparent black background |
| Click outside | Closes modal |
| Escape key | Closes modal |

### Playlist Sidebar

| Setting | Default | Description |
|---------|---------|-------------|
| Show Sidebar | Yes | Show playlist navigation |
| Sidebar Width | 350px | Width of playlist sidebar |

## Player Sources

### Supported Platforms

| Platform | Embed Type | Features |
|----------|------------|----------|
| YouTube | IFrame API | Full control, progress tracking |
| Vimeo | Player API | Full control, progress tracking |
| SoundCloud | Widget API | Full control, progress tracking |
| Archive.org | IFrame | Basic playback |
| Direct URL | HTML5 | Full control |

### Duration Fetching

| Platform | Method |
|----------|--------|
| YouTube | Requires API key (Settings → Advanced) |
| Vimeo | Automatic via oEmbed |
| SoundCloud | Automatic via API |
| Direct | Read from file metadata |

## Keyboard Shortcuts

Players support keyboard control:

| Key | Action |
|-----|--------|
| Space | Play/Pause |
| Left Arrow | Seek back 5s |
| Right Arrow | Seek forward 5s |
| Up Arrow | Volume up |
| Down Arrow | Volume down |
| M | Mute/Unmute |
| F | Toggle fullscreen |

## Progress Tracking

### Automatic Saving

Progress saves automatically:

- Every 5 seconds during playback
- On pause
- On modal close

### Resume Playback

When returning to a video:

1. Plugin checks saved progress
2. Resumes from last position
3. Shows in "Continue Watching"

### Completion

- Videos >= 90% complete marked as finished
- Removed from "Continue Watching"
- Progress indicator shows completion

## CSS Customization

### Player Container

```css
.mindful-media-player-container {
    background: #000;
    border-radius: 8px;
    overflow: hidden;
}
```

### Controls

```css
/* Custom play button */
.mindful-media-play-button {
    background: rgba(0, 0, 0, 0.7);
    border-radius: 50%;
}

/* Progress bar */
.mindful-media-progress-bar {
    height: 4px;
    background: var(--mindful-media-progress-color);
}
```

## Troubleshooting

### Video Not Playing

1. Check video URL is valid
2. Verify platform allows embedding
3. Check browser console for errors

### Progress Not Saving

1. User must be logged in
2. Check database table exists
3. Verify AJAX endpoints working

### Audio Controls Wrong Color

1. Clear browser cache
2. Verify progress color setting saved
3. Check CSS variables are loading
