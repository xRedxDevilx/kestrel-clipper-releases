# Publishing

## Who posts your clips

Kestrel does not post to TikTok, Instagram or YouTube itself. It hands the finished video to a service
that does. Two are built in.

| Backend | What you need | Notes |
|---|---|---|
| **Upload-Post** (default) | An API key and a profile name from app.upload-post.com | Their **free tier cannot connect TikTok at all.** If TikTok posts fail with "no account configured", that is why, not a bug in Kestrel |
| **My own tool (webhook)** | One https address | Point it at Postiz, Blotato, n8n, Make, or your own script. Nothing goes to Upload-Post |

Instagram can also go straight from your PC through Meta's own API, free, under **Advanced** on the
Publishing tab. It needs a Meta developer app, so most people should leave it alone.

## Writing a webhook receiver

Kestrel sends one multipart POST per clip:

| Field | What it is |
|---|---|
| `video` | the finished vertical MP4 |
| `title` | the short title |
| `platforms` | comma-separated, e.g. `tiktok,instagram` |
| `clip` | the file name |
| `<platform>_title` | the caption for each platform asked for |
| `youtube_description` | only when YouTube is one of the platforms |
| `X-Kestrel-Secret` (header) | the shared secret, if you set one |

**Answer 2xx** and every platform asked for counts as posted. That is enough for a shell script.

**Answer per-platform receipts** and each platform is tracked separately, so a later retry only retries
what failed:

```json
{"results": {"tiktok":    {"success": true,  "id": "7123..."},
             "instagram": {"success": false, "error": "no account connected"}}}
```

Set a shared secret unless your receiver is on a private network. Without one, anyone who learns the
address can post to your tool.

## Platform marks

The marks on the Publishing tab are each platform's own trademarks, from its official brand pack, used
under that platform's guidelines and **scaled only** - never recoloured, cropped or restyled. They are
not Kestrel Clipper's marks and are not covered by this project's licence.

`autoclipper/static/brand/README.md` records exactly which file each came from and how it was scaled, so
the provenance is auditable and a future resize starts from the original pack rather than from a
re-edited copy.

YouTube's icon is a rounded rectangle rather than a square, so it is scaled by height and keeps its own
aspect ratio - cropping or padding it square would be altering the mark.

Each platform can change its guidelines, and they govern what may be done with these files:

- TikTok: https://www.tiktok.com/about/brand-guidelines
- Instagram / Meta: https://about.meta.com/brand/resources/instagram/instagram-brand/
- YouTube: https://www.youtube.com/howyoutubeworks/resources/brand-resources/

## Daily caps

TikTok 15, YouTube 10, Instagram 50 per day. Kestrel stops before the cap rather than letting a post be
rejected.

## YouTube only gets your own content

Raw re-uploads of someone else's stream never go to YouTube, whatever you tick. YouTube treats them as
reused content and can demonetise the channel. Voice-over reels and clips carrying your own AI
commentary do go there.
