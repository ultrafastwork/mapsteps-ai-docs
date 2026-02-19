# WP Video Popup — Manual Test Cases

Covers both the **free** (`responsive-youtube-vimeo-popup`) and **pro** (`wp-video-popup-pro`) versions.

---

## How to Use

1. Create a test page/post in WordPress.
2. Open the block editor, click the **three-dot menu (⋮) → Code editor** (or press `Ctrl+Shift+Alt+M`).
3. Paste the block markup below directly into the code editor.
4. Switch back to Visual editor and preview the page.

---

## Free Version

### Default Trigger Block

Used for all free version tests unless stated otherwise. Paste this **once per test page**, alongside the shortcode block.

```
<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open Popup</a></p>
<!-- /wp:paragraph -->
```

---

### YouTube

#### 1. Basic YouTube

```
<!-- wp:shortcode -->
[wp-video-popup video="https://www.youtube.com/watch?v=YlUKcNNmywk"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open YouTube Popup</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Popup opens, YouTube video plays with autoplay.

---

#### 2. YouTube short URL

```
<!-- wp:shortcode -->
[wp-video-popup video="https://youtu.be/YlUKcNNmywk"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open YouTube Short URL</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Short URL correctly parsed, video plays.

---

#### 3. YouTube nocookie

```
<!-- wp:shortcode -->
[wp-video-popup video="https://www.youtube-nocookie.com/embed/YlUKcNNmywk"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open YouTube Nocookie</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Embeds from `youtube-nocookie.com`, not `youtube.com`.

---

#### 4. YouTube — muted

```
<!-- wp:shortcode -->
[wp-video-popup video="https://www.youtube.com/watch?v=YlUKcNNmywk" mute="1"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open Muted YouTube</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Video plays silently.

---

#### 5. YouTube — start at specific time

```
<!-- wp:shortcode -->
[wp-video-popup video="https://www.youtube.com/watch?v=YlUKcNNmywk" start="30"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open YouTube at 0:30</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Video starts at 0:30.

---

#### 6. YouTube — hide related videos

```
<!-- wp:shortcode -->
[wp-video-popup video="https://www.youtube.com/watch?v=YlUKcNNmywk" hide-related="1"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open YouTube Hide Related</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Related videos from same channel shown at end (YouTube no longer allows full suppression since 2018).

---

#### 7. YouTube — combined attributes

```
<!-- wp:shortcode -->
[wp-video-popup video="https://www.youtube.com/watch?v=4wZmRQcIDME" mute="1" start="15" hide-related="1"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open YouTube Combined</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Starts at 0:15, muted, related from same channel.

---

### Vimeo

#### 8. Vimeo — public

```
<!-- wp:shortcode -->
[wp-video-popup video="https://vimeo.com/136696258"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open Vimeo</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Vimeo video plays.

---

#### 9. Vimeo — private (hash in URL path)

```
<!-- wp:shortcode -->
[wp-video-popup video="https://vimeo.com/1122224382/a6f0498bb8"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open Private Vimeo (path hash)</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Private Vimeo video plays.

---

#### 10. Vimeo — private (hash as query param)

```
<!-- wp:shortcode -->
[wp-video-popup video="https://vimeo.com/1122224382?h=a6f0498bb8"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open Private Vimeo (query hash)</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Private Vimeo video plays.

---

#### 11. Vimeo — embed format URL

```
<!-- wp:shortcode -->
[wp-video-popup video="https://player.vimeo.com/video/136696258"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open Vimeo Embed URL</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Correctly parsed, video plays.

---

#### 12. Vimeo — muted

```
<!-- wp:shortcode -->
[wp-video-popup video="https://vimeo.com/136696258" mute="1"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open Muted Vimeo</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Vimeo plays silently.

---

#### 13. Vimeo — start at specific time

```
<!-- wp:shortcode -->
[wp-video-popup video="https://vimeo.com/136696258" start="20"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open Vimeo at 0:20</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Vimeo starts at 0:20.

---

#### 14. Vimeo — portrait mode

```
<!-- wp:shortcode -->
[wp-video-popup video="https://vimeo.com/136696258" portrait="1"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open Vimeo Portrait</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Popup renders in portrait (vertical) aspect ratio.

---

### Rumble

#### 15. Rumble — embed URL

```
<!-- wp:shortcode -->
[wp-video-popup video="https://rumble.com/embed/v4j2rri/?pub=4"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open Rumble Embed</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Rumble video plays.

---

#### 16. Rumble — direct URL

```
<!-- wp:shortcode -->
[wp-video-popup video="https://rumble.com/v4j2rri-some-title.html"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open Rumble Direct URL</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Rumble video plays (uses Iframely API fallback internally).

---

### Backward Compatibility

#### 17. Legacy shortcode alias

```
<!-- wp:shortcode -->
[ryv-popup video="https://www.youtube.com/watch?v=YlUKcNNmywk"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open via Legacy Shortcode</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Works identically to `[wp-video-popup]`.

---

#### 18. Legacy trigger class

```
<!-- wp:shortcode -->
[wp-video-popup video="https://www.youtube.com/watch?v=YlUKcNNmywk"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"ryv-popup"} -->
<p class="ryv-popup"><a href="#">Open via Legacy Trigger Class</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Opens the popup using the legacy `ryv-popup` trigger class.

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

### Default Trigger Block

```
<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open Popup</a></p>
<!-- /wp:paragraph -->
```

For targeted popups, use the popup `id` as the trigger class:

```
<!-- wp:paragraph {"className":"my-id"} -->
<p class="my-id"><a href="#">Open Specific Popup</a></p>
<!-- /wp:paragraph -->
```

---

### Multiple Popups & ID Targeting

#### 19. Multiple popups — targeted by ID

```
<!-- wp:shortcode -->
[wp-video-popup id="video-a" video="https://www.youtube.com/watch?v=YlUKcNNmywk"]
<!-- /wp:shortcode -->

<!-- wp:shortcode -->
[wp-video-popup id="video-b" video="https://vimeo.com/136696258"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"video-a"} -->
<p class="video-a"><a href="#">Open YouTube</a></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph {"className":"video-b"} -->
<p class="video-b"><a href="#">Open Vimeo</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Each trigger opens its own popup independently.

---

#### 20. Popup ID starting with a number

```
<!-- wp:shortcode -->
[wp-video-popup id="1video" video="https://www.youtube.com/watch?v=YlUKcNNmywk"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"1video"} -->
<p class="1video"><a href="#">Open Popup (numeric ID)</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Works correctly (uses `[class~="1video"]` selector internally).

---

#### 21. Default trigger with multiple popups on page

```
<!-- wp:shortcode -->
[wp-video-popup id="video-a" video="https://www.youtube.com/watch?v=YlUKcNNmywk"]
<!-- /wp:shortcode -->

<!-- wp:shortcode -->
[wp-video-popup id="video-b" video="https://vimeo.com/136696258"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open First Popup</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Opens the first popup (`video-a`).

---

### Autoplay on Page Load

#### 22. Autoplay on page load

```
<!-- wp:shortcode -->
[wp-video-popup autoplay="1" video="https://www.youtube.com/watch?v=4wZmRQcIDME"]
<!-- /wp:shortcode -->
```

✅ Expect: Popup opens automatically when the page loads. No trigger needed.

---

### Self-Hosted Videos

#### 23. Self-hosted video — basic

> Replace the URL with a real `.mp4` URL accessible from your server.

```
<!-- wp:shortcode -->
[wp-video-popup video="https://your-domain.com/path/to/video.mp4"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open Self-Hosted Video</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: `<video>` element used instead of iframe, video plays with controls.

---

#### 24. Self-hosted — muted + start time

> Replace the URL with a real `.mp4` URL accessible from your server.

```
<!-- wp:shortcode -->
[wp-video-popup video="https://your-domain.com/path/to/video.mp4" mute="1" start="10"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open Self-Hosted Muted at 10s</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Starts at 10s, muted.

---

### Video Galleries

#### 25. Gallery — basic (2 videos)

```
<!-- wp:shortcode -->
[wp-video-popup gallery="my-gallery" video="https://www.youtube.com/watch?v=YlUKcNNmywk"]
<!-- /wp:shortcode -->

<!-- wp:shortcode -->
[wp-video-popup gallery="my-gallery" video="https://vimeo.com/136696258"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open Gallery</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Gallery opens at first video, prev/next arrows navigate between videos.

---

#### 26. Gallery — 3 videos (mixed providers)

```
<!-- wp:shortcode -->
[wp-video-popup gallery="mixed-gallery" video="https://www.youtube.com/watch?v=YlUKcNNmywk"]
<!-- /wp:shortcode -->

<!-- wp:shortcode -->
[wp-video-popup gallery="mixed-gallery" video="https://vimeo.com/136696258"]
<!-- /wp:shortcode -->

<!-- wp:shortcode -->
[wp-video-popup gallery="mixed-gallery" video="https://rumble.com/embed/v4j2rri/?pub=4"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open Mixed Gallery</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: 3-video gallery, prev/next arrows work, keyboard left/right arrow navigation works, Escape closes.

---

#### 27. Gallery — autoplay on page load

```
<!-- wp:shortcode -->
[wp-video-popup gallery="auto-gallery" autoplay="1" video="https://www.youtube.com/watch?v=4wZmRQcIDME"]
<!-- /wp:shortcode -->

<!-- wp:shortcode -->
[wp-video-popup gallery="auto-gallery" video="https://vimeo.com/136696258"]
<!-- /wp:shortcode -->
```

✅ Expect: Gallery opens automatically on page load at the first video.

---

#### 28. Gallery — single item (fallback to regular popup)

```
<!-- wp:shortcode -->
[wp-video-popup gallery="solo" video="https://www.youtube.com/watch?v=YlUKcNNmywk"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open Solo Gallery</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Opens as a regular popup with no arrows (gallery with 1 item falls back gracefully).

---

### Portrait Mode

#### 29. Portrait mode

```
<!-- wp:shortcode -->
[wp-video-popup portrait="1" video="https://vimeo.com/136696258"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"wp-video-popup"} -->
<p class="wp-video-popup"><a href="#">Open Portrait Popup</a></p>
<!-- /wp:paragraph -->
```

✅ Expect: Popup renders in portrait (vertical) aspect ratio, no `is-resizable` class applied.

---

### All Shortcode Attributes Combined (Pro)

#### 30. Full attribute test

```
<!-- wp:shortcode -->
[wp-video-popup id="full-test" mute="1" start="10" hide-related="1" video="https://www.youtube.com/watch?v=4wZmRQcIDME"]
<!-- /wp:shortcode -->

<!-- wp:paragraph {"className":"full-test"} -->
<p class="full-test"><a href="#">Open Full Attribute Test</a></p>
<!-- /wp:paragraph -->
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
