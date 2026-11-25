# Changelog

## 1.3.5 - 25 November 2026

- Quit from the tray now closes the dashboard window and the app. The window is opened under the app's own browser profile, so it is a process Kestrel owns and can close; anything still recording is stopped and the process always exits.
- Closing the window leaves the app clipping in the tray and says so once, from the tray icon. A new setting in Settings makes closing the window quit instead.
- Updates install from inside the app: Download update fetches the installer, checks it against the checksum in the update manifest, and Install and restart runs it. The old button opened a release page that returned 404 for anyone but the owner.
- A download that does not match its checksum, or that is not an installer at all, is deleted and refused.
- Updating over a running copy no longer shows "Setup was unable to automatically close all applications": Setup closes the app, its helper and their ffmpeg and streamlink processes itself, and waits for Windows to release the files.
- A silent update starts the app again when it finishes.
- Downloads and release notes now come from the public releases repository.

## 1.3.4 - 21 November 2026

- Evaluate live reel ideas independently from clip excitement. The live watcher no longer inherits the clip judge's rejection policy, so a calm feature demonstration can produce a useful original reel idea.
- Give ideas their own evidence and usefulness rubric across games and discussion topics. Preserve the owner's save threshold, duplicate filtering and collection toggle; do not add extra AI requests.
- Keep the existing viral-clip judge and its approval rules unchanged.

## 1.3.3 - 21 November 2026

- Explicitly validate the optional TLS key-log path in frozen Python, where ignore_environment caused the default SSL context to skip the setting.
- Includes the connection, campaign, layout and attribution fixes from 1.3.2. The 1.3.2 Windows build was blocked by the new packaging check and no installer was published.

## 1.3.2 - 21 November 2026

- Recover from an inaccessible inherited TLS key-log path in the app and recorder helper, without changing Windows settings or disabling HTTPS certificate verification.
- Show failed live checks as unknown, and explain failed checks on Today instead of reporting everyone offline.
- Expand the dashboard to fill maximized windows.
- Import public linked campaign rule sheets; accept a published rules link when the campaign site hides references behind sign-in. Preserve unknown rules and manually edited fields.
- Credit Twitch clip broadcasters instead of the viewers who created clips when analysing online videos or converting clips without an explicit channel.
- Verify TLS recovery in both packaged Windows executables before attaching the installer.

## 1.3.1 - 20 November 2026

- Re-enabling a streamer’s auto-start choice clears a temporary hold left by an individual start after global pause.
- Includes all streamer, end-card, campaign and UI improvements from 1.3.0.


## 1.3.0 - 20 November 2026

### Streamer controls
- Live is now Streamers, with automatic Twitch, YouTube and Kick profile photos, red live indicators and orange clipping status.
- Individual start/pause and auto-start selection work independently of global pause. Paused channels still show live availability and activity.
- Today prioritises live streamers and processing clips. Review adds streamer, game/topic and Hot clip filters.

### Editing
- Recipe is now Edit style. End cards have editable headlines, supporting text, duration and colours, with neutral follow/watch/custom presets.
- Canvas and real renders share settings, including classic layouts. Campaign no-logo restrictions continue to suppress end cards.

### Campaigns
- Paste supported Content Rewards or Whop campaign links to fetch public details into an editable review form. Missing or membership-only rules remain flagged.
- Search real public Content Rewards listings by name/category or matches to added streamers. Saved campaigns are excluded from discovery results.
- Imports preserve minimum clip views and creator eligibility notes without inventing pool-unlock targets. Review and link streamers before saving.

### Usability
- Clearer publishing setup, local AI quality guidance and actual Ollama image-capability reporting.
- Settings navigation, save feedback, larger review cards and explanations for unavailable controls.
- Fixed start/pause races while metadata checks are in flight, and manual clipping after a pause.



## 1.2.0 - 19 November 2026

### Added
- **Stream content detection:** Live and Today show whether a stream is gaming, Just Chatting, reacting, IRL or another activity, with the identified game or discussion topic. Existing AI watch and clip-analysis requests supply the context; no separate background AI request is added.
- Context is saved on individual live and VOD clips and shown in Review. Low-confidence or missing results fall back to platform metadata rather than inventing a topic. Live title/category changes refresh without starting another recorder.
- Hot shorts keep source footage for the trim editor and can carry the Recipe's optional commentary voice-over.

### Fixed
- **Hot shorts disappearing:** live hourly replacement and low-score cleanup no longer delete manually selected Hot clips. Explicit rejection expiry still works normally.
- VOD shorts retain their configured streamer and campaign association using canonical channel identities. Campaign no-logo rules apply to VODs, story clips, Hot shorts and re-edits; no-AI campaigns suppress generated commentary.
- Post kits and uploads preserve the title, caption, credit and hashtags generated without an AI verdict.
- YouTube eligibility is enforced in the publisher: raw stream reposts are excluded even when YouTube is selected. Voice-over reels and clips with actual commentary remain eligible.
- Hot conversion applies campaign branding restrictions, generates configured commentary and uses unique output names.
- Diagnostics redact bearer/basic/API-key authorization headers, cookies, URL credentials and token-bearing query values, including quoted log formats.
- Clarified that Windows DPAPI protects against another user/machine, not programs running as the same Windows user.

### Updating
- Quit Kestrel Clipper before running the new Setup executable. Your local settings and clips are retained.
- Cloud posting/Telegram delivery still require connected accounts. Content labels are evidence-based estimates; review videos before publishing.

## 1.1.1 - November 2026

Fixes from a full test of 1.1.0 on a real Windows PC with live streams.

### Fixed
- **Captions missing on every clip** - the speech model couldn't open its own files on Windows (Hugging Face cache
  symlinks). It now lives as plain files in the app's data folder, repairs a broken download, and a failure is logged
  instead of silently producing clips without captions. PCs without an NVIDIA card skip the GPU attempt.
- **YouTube chat never connected** in the installed app (a data file was missing from the build).
- **Hot clips** ignored paused streamers and said "Add some Twitch streamers first". It now uses every Twitch streamer,
  explains that it works whether they're live or not, shows thumbnails, and has **Make short**: download the clip and
  edit it with your Recipe - no Twitch key needed.
- **VOD analyser downloads** were ~25 KB/s on Twitch VODs (pieces fetched one at a time) - now 16 at once, with MB/speed shown.
- **Campaign briefs**: "submit within 48 hours" was read as 30 minutes, and windows over 24 h were cut to 24 h.
- **Review**: compact cards (6+ per row, details folded away); **Clip now** shows a Processing card immediately with the
  current step; "Post & submit" only on campaign clips ("Post kit" otherwise).
- **Without AI** clips now still get a hook, title, caption and hashtags built from what was said.
- **Hook card** sits on the line between facecam and gameplay instead of over the streamer's face.
- Pickiness settings save automatically; voice defaults to free Edge voices; readable VoiceStudio error; AI-only
  options are greyed out with "Needs AI" when no AI is set up; Instagram "Disconnect" only when connected.
- Visual: squashed/mismatched checkboxes, stray "null" on Today, cut-off template text, "UNKNOWN" permission tag,
  game shown from the stream title on YouTube/Kick, page links like #review.
- Malformed requests return a clear error instead of a crash; harmless Windows connection-reset tracebacks no longer flood the log.

### Security
- Other websites can no longer change anything in the app (cross-site POSTs are refused - only the dashboard can).
- Update links must be https.

### Updates
- Installs now check a public version file once a day and show **Download update** when a new version is out.

## 1.1.0 - November 2026

### New
- **AI commentary voice-over** - a narrator sets up each clip, reacts in a quiet moment and asks a question after the
  payoff; clip audio is ducked under the voice and the lines appear on screen. Clips with commentary may post to YouTube.
- **Recipe live preview** - a phone preview on bundled demo media that redraws on every option, template cards that play
  the demo, and **Render real preview**.
- **Custom templates** - start from a layout, set facecam top/bottom and height, drag the title, captions, handle and
  logo on the preview.
- **Kick support** - live checks, recording, live chat and VODs.
- **Story clips** - one short per VOD that joins 2-4 moments telling one story.
- **Hot clips** - Twitch clips taking off right now, ranked by views per hour, with *Scan VOD*.
- **YouTube "most replayed"** peaks used to rank VOD moments.
- **Launch-week safety holds** - spoilers, early violence, gambling, copyrighted music and muted audio are never auto-posted.
- **YuNet facecam detection** - finds side-on, tilted, dim and headset faces the old detector missed.
- **Branding** - show/hide handle and credit; logo upload now works.
- **Smaller installer** - NVIDIA's speech libraries download only on NVIDIA PCs, in the background.
- **Illustrated PDF guides** for setup, publishing, Telegram, AI, money and troubleshooting.

### Fixed
- The dashboard now refuses requests for other host names (DNS-rebinding protection).
- Turning on the brand logo no longer crashes rendering.
- Campaigns that ban logos now drop the logo as well as the handle.

