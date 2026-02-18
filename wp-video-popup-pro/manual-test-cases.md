# WP Video Popup — Manual Test Cases

Covers both the **free** (`responsive-youtube-vimeo-popup`) and **pro** (`wp-video-popup-pro`) versions.

---

## How to Use

1. Create a test page/post in WordPress.
2. Paste the shortcode(s) into the page content.
3. Add the trigger markup on the same page.
4. Preview the page and verify the expected behavior.

---

## Free Version

### Trigger Markup

Use this trigger for all free version tests (unless stated otherwise):

```html
<a href="#" class="wp-video-popup">Open Popup</a>
```

---

### YouTube

#### 1. Basic YouTube
```
[wp-video-popup video="https://www.youtube.com/watch?v=dQw4w9WgXcQ"]
```
✅ Expect: Popup opens, YouTube video plays with autoplay.

#### 2. YouTube short URL
```
[wp-video-popup video="https://youtu.be/dQw4w9WgXcQ"]
```
✅ Expect: Short URL correctly parsed, video plays.

#### 3. YouTube nocookie
```
[wp-video-popup video="https://www.youtube-nocookie.com/embed/dQw4w9WgXcQ"]
```
✅ Expect: Embeds from `youtube-nocookie.com`, not `youtube.com`.

#### 4. YouTube — muted
```
[wp-video-popup video="https://www.youtube.com/watch?v=dQw4w9WgXcQ" mute="1"]
```
✅ Expect: Video plays silently.

#### 5. YouTube — start at specific time
```
[wp-video-popup video="https://www.youtube.com/watch?v=dQw4w9WgXcQ" start="30"]
```
✅ Expect: Video starts at 0:30.

#### 6. YouTube — hide related videos
```
[wp-video-popup video="https://www.youtube.com/watch?v=dQw4w9WgXcQ" hide-related="1"]
```
✅ Expect: Related videos from same channel shown at end (YouTube no longer allows full suppression since 2018).

#### 7. YouTube — combined attributes
```
[wp-video-popup video="https://www.youtube.com/watch?v=dQw4w9WgXcQ" mute="1" start="15" hide-related="1"]
```
✅ Expect: Starts at 0:15, muted, related from same channel.

---

### Vimeo

#### 8. Vimeo — public
```
[wp-video-popup video="https://vimeo.com/136696258"]
```
✅ Expect: Vimeo video plays.

#### 9. Vimeo — private (hash in URL path)
```
[wp-video-popup video="https://vimeo.com/123456789/abcdef1234"]
```
✅ Expect: Private Vimeo video plays. Replace with a real private Vimeo URL you have access to.

#### 10. Vimeo — private (hash as query param)
```
[wp-video-popup video="https://vimeo.com/123456789?h=abcdef1234"]
```
✅ Expect: Private Vimeo video plays.

#### 11. Vimeo — embed format URL
```
[wp-video-popup video="https://player.vimeo.com/video/136696258"]
```
✅ Expect: Correctly parsed, video plays.

#### 12. Vimeo — muted
```
[wp-video-popup video="https://vimeo.com/136696258" mute="1"]
```
✅ Expect: Vimeo plays silently.

#### 13. Vimeo — start at specific time
```
[wp-video-popup video="https://vimeo.com/136696258" start="20"]
```
✅ Expect: Vimeo starts at 0:20.

#### 14. Vimeo — portrait mode
```
[wp-video-popup video="https://vimeo.com/136696258" portrait="1"]
```
✅ Expect: Popup renders in portrait (vertical) aspect ratio.

---

### Rumble

#### 15. Rumble — embed URL
```
[wp-video-popup video="https://rumble.com/embed/v4j2rri/?pub=4"]
```
✅ Expect: Rumble video plays.

#### 16. Rumble — direct URL
```
[wp-video-popup video="https://rumble.com/v4j2rri-some-title.html"]
```
✅ Expect: Rumble video plays (uses Iframely API fallback internally).

---

### Backward Compatibility

#### 17. Legacy shortcode alias
```
[ryv-popup video="https://www.youtube.com/watch?v=dQw4w9WgXcQ"]
```
✅ Expect: Works identically to `[wp-video-popup]`.

#### 18. Legacy trigger class
```html
<a href="#" class="ryv-popup">Open Popup</a>
```
✅ Expect: Opens the popup.

---

### Close Behaviors

After opening any popup above:

| Action | Expected |
|---|---|
| Click the **X button** | Closes popup, video stops |
| Click the **dark overlay** | Closes popup, video stops |
| Press **Escape key** | Closes popup, video stops |
| Reopen popup | Video restarts from beginning (src cleared on close) |

---

## Pro Version

### Trigger Markup

Default trigger (targets first popup on page):

```html
<a href="#" class="wp-video-popup">Open Popup</a>
```

Targeted trigger (replace `my-id` with the `id` used in the shortcode):

```html
<a href="#" class="my-id">Open Specific Popup</a>
```

---

### Multiple Popups & ID Targeting

#### 19. Multiple popups — targeted by ID
```
[wp-video-popup id="video-a" video="https://www.youtube.com/watch?v=dQw4w9WgXcQ"]
[wp-video-popup id="video-b" video="https://vimeo.com/136696258"]
```
```html
<a href="#" class="video-a">Open YouTube</a>
<a href="#" class="video-b">Open Vimeo</a>
```
✅ Expect: Each trigger opens its own popup independently.

#### 20. Popup ID starting with a number
```
[wp-video-popup id="1video" video="https://www.youtube.com/watch?v=dQw4w9WgXcQ"]
```
```html
<a href="#" class="1video">Open Popup</a>
```
✅ Expect: Works correctly (uses `[class~="1video"]` selector internally).

#### 21. Default trigger with multiple popups on page
```
[wp-video-popup id="video-a" video="https://www.youtube.com/watch?v=dQw4w9WgXcQ"]
[wp-video-popup id="video-b" video="https://vimeo.com/136696258"]
```
```html
<a href="#" class="wp-video-popup">Open First Popup</a>
```
✅ Expect: Opens the first popup (`video-a`).

---

### Autoplay on Page Load

#### 22. Autoplay on page load
```
[wp-video-popup autoplay="1" video="https://www.youtube.com/watch?v=dQw4w9WgXcQ"]
```
✅ Expect: Popup opens automatically when the page loads (no trigger click needed).

---

### Self-Hosted Videos

#### 23. Self-hosted video — basic
```
[wp-video-popup video="https://your-domain.com/path/to/video.mp4"]
```
✅ Expect: `<video>` element used instead of iframe, video plays with controls.

#### 24. Self-hosted — muted + start time
```
[wp-video-popup video="https://your-domain.com/path/to/video.mp4" mute="1" start="10"]
```
✅ Expect: Starts at 10s, muted.

---

### Video Galleries

#### 25. Gallery — basic (2 videos)
```
[wp-video-popup gallery="my-gallery" video="https://www.youtube.com/watch?v=dQw4w9WgXcQ"]
[wp-video-popup gallery="my-gallery" video="https://vimeo.com/136696258"]
```
```html
<a href="#" class="wp-video-popup">Open Gallery</a>
```
✅ Expect: Gallery opens at first video, prev/next arrows navigate between videos.

#### 26. Gallery — 3 videos (mixed providers)
```
[wp-video-popup gallery="mixed-gallery" video="https://www.youtube.com/watch?v=dQw4w9WgXcQ"]
[wp-video-popup gallery="mixed-gallery" video="https://vimeo.com/136696258"]
[wp-video-popup gallery="mixed-gallery" video="https://rumble.com/embed/v4j2rri/?pub=4"]
```
```html
<a href="#" class="wp-video-popup">Open Gallery</a>
```
✅ Expect: 3-video gallery, prev/next arrows work, keyboard left/right arrow navigation works, Escape closes.

#### 27. Gallery — autoplay on page load
```
[wp-video-popup gallery="auto-gallery" autoplay="1" video="https://www.youtube.com/watch?v=dQw4w9WgXcQ"]
[wp-video-popup gallery="auto-gallery" video="https://vimeo.com/136696258"]
```
✅ Expect: Gallery opens automatically on page load at the first video.

#### 28. Gallery — single item (fallback to regular popup)
```
[wp-video-popup gallery="solo" video="https://www.youtube.com/watch?v=dQw4w9WgXcQ"]
```
```html
<a href="#" class="wp-video-popup">Open</a>
```
✅ Expect: Opens as a regular popup with no arrows (gallery with 1 item falls back gracefully).

---

### Portrait Mode

#### 29. Portrait mode
```
[wp-video-popup portrait="1" video="https://vimeo.com/136696258"]
```
✅ Expect: Popup renders in portrait (vertical) aspect ratio, no `is-resizable` class applied.

---

### All Shortcode Attributes Combined (Pro)

#### 30. Full attribute test
```
[wp-video-popup id="full-test" mute="1" start="10" hide-related="1" video="https://www.youtube.com/watch?v=dQw4w9WgXcQ"]
```
```html
<a href="#" class="full-test">Open Full Test</a>
```
✅ Expect: Starts at 0:10, muted, related from same channel.

---

## Cross-Version Behaviors to Verify

| Behavior | How to test |
|---|---|
| **GDPR compliance** | Open browser DevTools → Network tab. No video request should appear until trigger is clicked. |
| **Responsive** | Resize browser window while popup is open — video should resize accordingly. |
| **Video stops on close** | Close popup, reopen — video should restart from beginning. |
| **No double-encoded URL params** | Inspect the `data-wp-video-popup-url` attribute in DevTools — should contain `&` not `&amp;`. |
| **Private Vimeo** | Use a real private Vimeo URL with hash — should embed correctly without stripping the hash. |
