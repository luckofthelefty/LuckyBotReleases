# LuckyBot

A desktop app for Twitch streamers. From a single window it runs alert overlays, a talking avatar, a full multi-channel chat client, a native chatbot, subathons, moderation tools, channel points, polls and predictions, OBS and Home Assistant control, closed captions with transcripts, and a clip manager. It runs entirely on your machine with a local server and embedded database, and installs in under 100 MB.

LuckyBot connects to Twitch directly with your login. No Streamer.bot required, though connecting one adds more sources. A free [LuckyBot Cloud](https://cloud.luckybot.app) account installs overlays shared with a link and gives you chat and your activity feed in any browser. A subscription adds Ko-fi, Streamlabs, StreamElements, Fourthwall, and custom WebSocket events, the remote Deck, remote OBS control, and sharing your own overlays.

![LuckyBot home](docs/images/home.png)
<!-- shot: home.png | /home | same image as getting-started: Home with the connection status strip and Running now -->

---

## How it works

1. Launch the app. The local server and database start automatically.
2. Log in with Twitch. Events, chat, and channel actions work natively from there.
3. Create an overlay using the drag-and-drop editor, the HTML/CSS/JS code sandbox, a widget, a reactive character, a talking avatar, or a ready-made starter.
4. Copy the overlay URL and paste it into OBS as a Browser Source.
5. When an event comes in, the matching alert plays.

Optional: connect Streamer.bot over a local WebSocket, or add a LuckyBot Cloud token in Settings. When multiple sources deliver the same event, LuckyBot fires exactly one alert, preferring Twitch's own feed first, then Streamer.bot, then Cloud.

---

## Features

Overlays
- Drag-and-drop visual editor with layers, shapes, groups, motion paths, attachments, animations, keyframe timelines, and a properties panel
- Reactive overlays: a character with a looping idle animation and a reaction per event
- Avatar overlays (PNGTuber): a character whose mouth follows your voice, from a microphone or an OBS audio source, with a hop when you start talking and a blink of its own
- A Visualizer layer that draws your sound as spectrum bars, an LED meter, or a wave
- Full HTML/CSS/JS code sandbox with live preview, configurable fields, a console, and one-click template updates
- Ready-made templates: stream alerts, goal widgets, Spotify now playing, Twitch polls and predictions, subathon timer and goals, weather, sound alerts, and more
- Widget overlays that stay on screen and update live: sub, bits, and follower goals, chatbot counters, and every Stats page variable
- Import your StreamElements overlays and AlertBox, media included
- Export overlays as .beacon files, with an option to bundle media; import by drag and drop
- Share any overlay with a link, images, sounds, and video included (sharing needs a LuckyBot Cloud subscription; installing needs a free cloud account)
- Guided tours for your first overlay, the alert editor, and the chatbot Blueprint
- A Content Security Policy on every overlay page, with an in-app security notice if a page ever runs script it should not

Alerts
- Multiple alerts per overlay, each bound to one or more event types
- Weighted chance, variants with conditional logic, priority or random selection
- Per-alert duration, queue behavior, chaining, and optional text-to-speech
- Show and hide animations per layer, plus a keyframe animator for full timelines
- Blocking and non-blocking queues with pause, skip, clear, and mute controls, and a floating Deck to fire alerts by hand

Chat
- Full chat client for your channel: badges, emotes, cheermotes, replies, deleted-message handling, translation, and first-time-chatter highlights
- Moderate other channels in tabs, with mod actions, pins, polls, hype train and ad timers per channel
- Shared chat sessions show a participant banner and attribute messages to their source channel
- TikTok LIVE chat and gifts alongside Twitch
- Pop out any chat to its own window, dock it in OBS, or add styled chat overlays to OBS that restyle live
- 7TV name paints, off until you turn them on, in chat windows and the OBS chat overlay

Chatbot
- Custom commands with variables, cooldowns, permission levels, costs, and counters (deaths, wins, anything)
- Blueprint: commands, timers, and walk ons open as a graph where every step is a node, with Branch and Split steps and values you drag from one step onto another
- Advanced actions: more than thirty steps including conditions, fetches, variables, delays, OBS control, Lumia Stream lights, Home Assistant devices, Spotify, key presses, currency, custom scripts, and sound alerts, from a single command
- Event triggers: commands that fire on subs, raids, cheers, follows, and thon grants
- Counters can be dropped onto an overlay in one click and update live as commands run
- Timed messages with cycling groups and spacing, walk ons, viewer queues, and quotes
- A currency with a shop, watch time tracking, casino games, and a builder for your own session minigames (ghost guessing, raffles, closest number)
- Spotify song requests from chat, with mod controls and a fallback playlist
- Import commands, timers, quotes, counters, and balances from Firebot, StreamElements, Nightbot, Streamlabs Cloudbot, Streamlabs Chatbot, and Mix It Up
- Spam filters and banned words
- Runs from your own account or a separate bot account, server-side, even with the dashboard closed

Thons
- Subathons and point-a-thons run on the server, so OBS reloads and crashes never lose the clock
- Rules per event and tier, happy-hour multipliers, milestone goals, an undo log, and a setup wizard
- Subathon Timer and Thon Goals overlays

Activity feed
- Live feed of events from every connected source, with per-service tabs and filters
- Chips under each event show what it set off: the alert that played, the command that ran, the subathon time it added
- Expand any event to see the full payload; replay past events and see which overlays the replay reached; run it as an OBS dock
- Customize badge labels, display templates, and colors per event type

Stream tools
- Home page with a connection status strip, what is running now, and stream title, category, and tag editing
- Polls, predictions, and channel point reward management with a redemption queue
- Moderation page: unban requests and blocked terms
- Video Manager: create clips from VODs with your stream markers, browse and bulk-download clips
- OBS control: Studio mode with Preview and Program, transitions, scenes, sources, audio mixer, and streaming status over obs-websocket, plus automatic recovery of LuckyBot browser sources
- Home Assistant: a page for your lights, scenes, and devices, and a command step with a guard on what viewers may control
- Stats page with editable counts, goals, labels, leaderboards, and a choice of how subs are counted
- Closed captions from an on-device speech engine with punctuation, caption filters, a captions overlay set up in one click, guests who caption their own microphone, and a searchable transcript per stream

Media library
- Manage images, video, audio, and GIFs locally, with bulk select and delete
- Tracks which alerts use a file before you delete it

Other
- Text-to-speech via ElevenLabs, Amazon Polly, or TTS.Monster
- Spotify now-playing overlay and playback controls
- Connections for Streamer.bot, OBS, Lumia Stream, Home Assistant, Spotify, LuckyBot Cloud, StreamElements, TikTok LIVE, and TreatStream
- Six color themes that every page of the dashboard follows
- Embedded database with scheduled backups, self-healing recovery, and a backup before every update
- In-app feedback that goes straight to the developer

---

## Requirements

- Windows 10 or later (64-bit)
- OBS Studio or any software that supports browser sources
- A Twitch account

Optional:
- [Streamer.bot](https://streamer.bot) for YouTube and Kick events and anything else your Streamer.bot instance connects to
- A [LuckyBot Cloud](https://cloud.luckybot.app) account: free for installing shared overlays and for chat and the activity feed in a browser, a subscription for cloud-relayed events, the remote Deck and OBS control, and sharing overlays
- [Home Assistant](https://www.home-assistant.io) if you want your stream to run your lights and devices

---

## Install

Download the latest installer from the [Releases](https://github.com/luckofthelefty/LuckyBotReleases/releases) page and run it. The app updates itself automatically when new versions come out, taking a database backup first.

---

## Documentation

- [Getting Started](docs/getting-started.md)
- [Overlays](docs/overlays.md)
- [Alerts and Variants](docs/alerts-and-variants.md)
- [Visual Editor](docs/visual-editor.md)
- [Reactive Overlays](docs/reactive-overlays.md)
- [Avatar Overlays](docs/avatar-overlays.md)
- [Advanced Editor](docs/advanced-editor.md)
- [Widgets](docs/widgets.md)
- [Chat](docs/chat.md)
- [Chatbot](docs/chat-bot.md)
- [Commands](docs/commands.md)
- [Stream Tools](docs/stream-tools.md)
- [Home Assistant](docs/home-assistant.md)
- [Thons](docs/thons.md)
- [Activity Feed](docs/activity-feed.md)
- [Alert Queues](docs/queues.md)
- [Media Library](docs/media-library.md)
- [Settings](docs/settings.md)

---

## What's New

Recent highlights from the 0.6.3xx releases:

- Captions: a new on-device speech engine with punctuation, a transcript per stream with exports, caption filters by group, a captions overlay set up from the Captions page, and guests who caption their own microphone.
- Avatar overlays: a PNGTuber whose mouth follows your voice, and a Visualizer layer for static, reactive, and avatar overlays.
- Blueprint: commands, timers, and walk ons as a graph of steps, with Branch and Split, a value picker on every field, and values you drag onto a step.
- When, Only if, Do cards for commands, timers, walk ons, overlays, alerts, and thon rules, and one delete pop-up across the whole app.
- Home Assistant: a page for your devices and a command step, with a guard on what viewers may control.
- Share an overlay with a link, and free LuckyBot Cloud accounts for installing shared overlays and for chat and the activity feed in a browser.
- The Activity feed shows what each event set off, and Replay says what it reached.
- OBS page Studio mode with Preview, Program, and transitions.
- 7TV name paints in chat and the OBS chat overlay, and emotes that refresh on their own.
- Simpler thon rules that open with one number, and YouTube Super Chats and Gifts that count their value.
- Advanced overlays can control Lumia Stream lights, and Hype Train events carry the top contributors.
- Alert sounds and videos are cached when an overlay loads, so the first alert of the stream plays its sound.

The full changelog lives on the [Releases](https://github.com/luckofthelefty/LuckyBotReleases/releases) page.

---

## License

LuckyBot is free to use. Copyright 2026 LuckoftheLefty, all rights reserved. See [LICENSE](LICENSE).
