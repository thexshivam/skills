---
name: python
description: Process videos with the VideoDB Python SDK. Handles trimming, combining clips, audio overlays, background music, subtitles, transcription, voiceover, text/image overlays, transcoding, resolution change, aspect-ratio fix, resizing for social platforms, media generation, search, and real-time capture — all server-side with no ffmpeg or local encoding tools needed.
allowed-tools: Read Grep Glob Bash(python:*)
argument-hint: "[task description]"
---

# VideoDB Python Skill

Use this skill for VideoDB Python SDK workflows: upload, transcript, subtitle, search, timeline editing, generative media, and real-time capture.

**Do not use ffmpeg, moviepy, or local encoding tools** when VideoDB supports the operation. The following are all handled server-side by VideoDB — trimming, combining clips, overlaying audio or music, adding subtitles, text/image overlays, transcoding, resolution changes, aspect-ratio conversion, resizing for platform requirements, transcription, and media generation. Only fall back to local tools for operations listed under Limitations in reference/editor.md (transitions, speed changes, crop/zoom, colour grading, volume mixing).

### When to use what

| Problem | VideoDB solution |
|---------|-----------------|
| Platform rejects video aspect ratio or resolution | `video.reframe()` or `conn.transcode()` with `VideoConfig` |
| Need to resize video for Twitter/Instagram/TikTok | `video.reframe(target="vertical")` or `target="square"` |
| Need to change resolution (e.g. 1080p → 720p) | `conn.transcode()` with `VideoConfig(resolution=720)` |
| Need to overlay audio/music on video | `AudioAsset` on a `Timeline` |
| Need to add subtitles | `video.add_subtitle()` or `CaptionAsset` |
| Need to combine/trim clips | `VideoAsset` on a `Timeline` |
| Need to generate voiceover, music, or SFX | `coll.generate_voice()`, `generate_music()`, `generate_sound_effect()` |

## Setup

Run setup from the plugin root using absolute paths so it works regardless of current directory:

```bash
python "${CLAUDE_PLUGIN_ROOT}/python/scripts/setup_venv.py"
python "${CLAUDE_PLUGIN_ROOT}/python/scripts/check_connection.py"
```

## API Key

An API key from https://console.videodb.io is required.

```python
import videodb
from dotenv import load_dotenv

load_dotenv()
conn = videodb.connect()
coll = conn.get_collection()
```

If `VIDEO_DB_API_KEY` is not set and no key is passed to `videodb.connect()`, ask the user for it.

## Quick Reference

### Upload media

```python
# URL
video = coll.upload(url="https://example.com/video.mp4")

# YouTube
video = coll.upload(url="https://www.youtube.com/watch?v=VIDEO_ID")

# Local file
video = coll.upload(file_path="/path/to/video.mp4")
```

### Transcript + subtitle

```python
video.index_spoken_words()
text = video.get_transcript_text()
stream_url = video.add_subtitle()
```

### Search inside videos

```python
video.index_spoken_words()
results = video.search("product demo")
stream_url = results.compile()
```

### Scene search

```python
from videodb import SearchType, IndexType, SceneExtractionType

scene_index_id = video.index_scenes(
    extraction_type=SceneExtractionType.shot_based,
    prompt="Describe the visual content in this scene.",
)

results = video.search(
    query="person writing on a whiteboard",
    search_type=SearchType.semantic,
    index_type=IndexType.scene,
    scene_index_id=scene_index_id,
)
stream_url = results.compile()
```

### Timeline editing

```python
from videodb.timeline import Timeline
from videodb.asset import VideoAsset, TextAsset, TextStyle

timeline = Timeline(conn)
timeline.add_inline(VideoAsset(asset_id=video.id, start=10, end=30))
timeline.add_overlay(0, TextAsset(text="The End", duration=3, style=TextStyle(fontsize=36)))
stream_url = timeline.generate_stream()
```

### Transcode video (resolution / quality change)

```python
from videodb import TranscodeMode, VideoConfig, AudioConfig

# Change resolution, quality, or aspect ratio server-side
job_id = conn.transcode(
    source="https://example.com/video.mp4",
    callback_url="https://example.com/webhook",
    mode=TranscodeMode.economy,
    video_config=VideoConfig(resolution=720, quality=23, aspect_ratio="16:9"),
    audio_config=AudioConfig(mute=False),
)
```

### Reframe aspect ratio (for social platforms)

```python
from videodb import ReframeMode

# Fix aspect ratio for Twitter / X (landscape 16:9)
reframed = video.reframe(target="landscape", mode=ReframeMode.smart)

# Instagram Reels / TikTok (vertical 9:16)
reframed = video.reframe(target="vertical", mode=ReframeMode.smart)

# Square (1:1)
reframed = video.reframe(target="square")

# Custom dimensions
reframed = video.reframe(target={"width": 1280, "height": 720})
```

### Generative media

```python
image = coll.generate_image(
    prompt="a sunset over mountains",
    aspect_ratio="16:9",
)
```

## Error handling

```python
from videodb.exceptions import AuthenticationError, InvalidRequestError

try:
    conn = videodb.connect()
except AuthenticationError:
    print("Check your VIDEO_DB_API_KEY")

try:
    video = coll.upload(url="https://example.com/video.mp4")
except InvalidRequestError as e:
    print(f"Upload failed: {e}")
```

## Additional docs in this plugin

- `${CLAUDE_PLUGIN_ROOT}/python/reference/api-reference.md`
- `${CLAUDE_PLUGIN_ROOT}/python/reference/search.md`
- `${CLAUDE_PLUGIN_ROOT}/python/reference/editor.md`
- `${CLAUDE_PLUGIN_ROOT}/python/reference/generative.md`
- `${CLAUDE_PLUGIN_ROOT}/python/reference/meetings.md`
- `${CLAUDE_PLUGIN_ROOT}/python/reference/rtstream.md`
- `${CLAUDE_PLUGIN_ROOT}/python/reference/capture.md`
- `${CLAUDE_PLUGIN_ROOT}/python/reference/use-cases.md`
