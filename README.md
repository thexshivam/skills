[![GitHub stars](https://img.shields.io/github/stars/video-db/skills.svg?style=for-the-badge)](https://github.com/video-db/skills/stargazers)
[![Issues](https://img.shields.io/github/issues/video-db/videodb-python.svg?style=for-the-badge)](https://github.com/video-db/videodb-python/issues)
[![Website](https://img.shields.io/website?url=https%3A%2F%2Fvideodb.io%2F&style=for-the-badge&label=videodb.io)](https://videodb.io)

<div align="center">

<img width="1856" height="576" alt="github_banner_skills" src="https://github.com/user-attachments/assets/a99b59d1-62de-43be-afcd-af5347372db6" width="800"/>


**The only perception skill your agent needs.**

Works with **Claude Code**, **Cursor**, **Copilot**, and other AI agents

**[📚 Explore the Docs](https://docs.videodb.io)**

</div>



## Why add this Skill

This skill gives your agent one consistent interface to:

- **See**: Realtime desktop screen, mic and system audio, RTSP streams, ingest files, URLs, YouTube.

- **Understand**: Visual understanding, transcribe, index and search moments with playble clips

- **Act**: Stream results, trigger alerts on live feeds, edit timelines, generate subtitles and overlays, export clips.



## What it does

VideoDB Skills lets your AI coding agent run end to end, server-side video workflows in real time and batch:

- Capture desktop screen, mic, and system audio for real time processing.
- Upload and process RTSP streams, videos from YouTube, URLs, and local files.
- Create realtime context of visual and spoken information. 
- Index and search spoken words and visual scenes anytime.
- Generate transcripts, subtitles, and AI media.
- Edit clips, overlays, and exports server side.

Return playable HLS links for anything you build.


## Get Started

Get started in two quick steps. Open your AI coding agent (Requires **Python 3.9+**) and follow along.


### Step 1: Install the skill

```bash
npx skills add video-db/skills
```

Or install with Claude Code plugin:

```bash
/plugin marketplace add video-db/skills
/plugin install videodb@videodb-skills
```

### Step 2: Setup

```
/videodb setup
```

The agent will guide setup for your [VideoDB API key](https://console.videodb.io) ($20 free credits, no credit card required), install the SDK, and verify the connection.


> For Cursor, Copilot, and other agents, ask your agent to **"setup videodb"**

If needed, you can set API key in your current terminal session:

```bash
export VIDEO_DB_API_KEY=sk-xxx
```

---
## Give your agent instructions

Ask your agent to run instructions like these. The skill loads automatically.

- *"Upload https://www.youtube.com/watch?v=FgrO9ADPZSA and give me a summary"*
- *"Search for 'product demo' in my latest video"*
- *"Add subtitles with white text on black background"*
- *"Take clips from 10s-30s and 45s-60s, add a title card, and combine them"*
- *"Capture my screen and tell me what's happening in real-time"*
- *"Start recording my meeting and give me a summary of actionable points at the end"*
- *"Generate background music and overlay it on my video"*


---

## Capability
VideoDB is the server side video stack for agents and apps.
Run reliable, scalable, cost efficient workflows across realtime streams and batch video, with built in AI understanding, without wiring up ffmpeg glue.
Keep your client and agent stack light: send video in, get back structured context, searchable moments, and playable streams.

### When to use VideoDB
- Your app needs video workflows, but you do not want ffmpeg running everywhere
- You want realtime perception from RTSP feeds or desktop capture
- You need search by what was said or shown, then turn results into clips
- You want server side editing, reframing, subtitles, dubbing, and streaming links

| Capability              | What it unlocks                                                               |
| ----------------------- | ----------------------------------------------------------------------------- |
| **Capture**             | Capture desktop screen, mic, and system audio for realtime processing         |
| **Upload**              | Ingest video from YouTube, URLs, or local files                               |
| **Context**             | Generate realtime structured context for any RTSP feed or desktop stream      |
| **Search**              | Find exact moments by speech, scenes, or metadata, return playable evidence   |
| **Transcripts**         | Generate clean, timestamped transcripts from any video                        |
| **Subtitles**           | Auto generate subtitles, then style and burn in or export                     |
| **Edit**                | Trim, merge, clip, overlay text, images, audio, plus dubbing and translation  |
| **AI Generate**         | Create images, video, music, sound effects, and voiceovers from text          |
| **Transcode / Reframe** | Change resolution, quality, aspect ratio, and social crops, all on the server |
| **Stream**              | Get instant playable HLS links (built in CDN) for anything you ingest or generate.             |


### The idea in one line
See → Understand → Act, as an API, for video and audio.

**Supported Platforms:** macOS, Linux, Windows (PowerShell)

---

## Community & Support

- **Documentation:** [docs.videodb.io](https://docs.videodb.io)
- **Discord:** [Join our community](https://discord.com/invite/py9P639jGz)

<div align="center">

Made with ❤️ by the VideoDB team

</div>
