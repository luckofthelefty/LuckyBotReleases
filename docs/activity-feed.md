# Activity Feed

The activity feed shows stream events from every connected source in real time. Use it to monitor what is happening, replay events, and check event data when building alert conditions.

![Activity feed](images/activity.png)
<!-- shot: activity.png | /activity | the feed with set-off chips under events and the new header buttons (text size, lightning); use rows without real viewers' names or crop them out -->

---

## Event sources

Events arrive from up to three places:

- **Twitch**: native events from your Twitch login. Always active. TikTok LIVE and TreatStream events arrive here too when those connections are on.
- **Streamer.bot**: optional, over a local WebSocket. Adds YouTube events (including Super Chats, memberships, and YouTube Gifts), Kick events, and anything else your Streamer.bot connects to.
- **LuckyBot Cloud**: optional, via a cloud token and a subscription. Relays services such as Ko-fi, Streamlabs, StreamElements, Fourthwall, and custom WebSocket feeds.

All can be active at once; duplicate copies of the same event are collapsed automatically. A gift bomb that arrives from both Twitch and Streamer.bot shows as one row. While LuckyBot's own TreatStream connection is up, Streamer.bot's copy of a treat is ignored, so a treat shows once and fires your chatbot treat trigger once. Connections are set up in **Settings > Connections**.

The feed header shows the Streamer.bot connection state, a viewer-count pill (click to show or hide the number), an ad countdown during mid-rolls, a **Pop out** button for a separate window, a text size switch, the **Show what each event set off** button, and a **Copy OBS dock URL** button so the feed can run as a custom browser dock inside OBS. The popout has a **Keep this window on top** option.

The text size switch is three **A** buttons: Small, Normal, and Large. The main page, the popout, and the OBS dock each remember their own size.

---

## The event list

Each row shows the event type as a colored badge, the viewer's name, a summary (tier, months, amount, message), and the arrival time. Click a row to expand the full payload as key/value pairs. Gift bombs fold their individual gifted subs into one row.

**Mark all read** and **Clear history** live at the top of the feed. The feed keeps recent events between app restarts and pages older ones in batches of 200. Right-click a row to **Filter to this event** type temporarily.

### What each event set off

Under each event, chips show what it set off in LuckyBot: the alert it played (overlay and alert or variant name), the chatbot command it ran or skipped, the subathon time or points it added, and any thon goal it reached. The chips stay with the row after a restart.

The lightning button in the header turns the chips on and off. Each window remembers the choice.

<!-- shot: activity-set-off.png | /activity | a feed row (use a test or sample event, no real viewer names) with set-off chips under it: an alert chip and a command chip; also show the text size A buttons and the lightning button in the header -->

---

## Tabs

The tab bar groups events by service (Twitch, YouTube, and so on), plus an **All** tab. Click the **+** button to add or remove service tabs.

Right-click any service tab for:

- **Filter events**: a searchable list of that service's event types. Toggle each on or off, or use select all, deselect all, and reset to defaults. Noisy types like chat messages and viewer-count updates are hidden by default.
- **Remove tab**

---

## Replaying events

Click **Replay** on any event row to send that event through your overlays as if it had just arrived. Overlays evaluate variant conditions and queue matching alerts exactly like a live event. Replay works the same for events that came in through LuckyBot Cloud.

A line under the row then says what the replay reached, for example "Replayed on 1 open overlay. Listening for it: Stream Alerts / Cheer." When nothing played it says why:

- the alerts are paused,
- the overlays listening for it are not open in OBS or a browser,
- no alert listens for that event (it was still sent to your open overlays, so an advanced overlay can react to it).

A replay only plays alerts. Commands, chat messages, and subathon time are not run again, and the replay does not add set-off chips as if the event happened twice.

---

## Customizing event display

Click **Customize** on any expanded event row to change how that event type renders:

- **Label**: override the badge text.
- **User template** and **Meta template**: `{{fieldKey}}` templates for the name and summary columns, with insert buttons for the available fields.
- **Colors and sizes** for the badge, user text, and meta text.

Click **Reset** to remove the customizations for that type. Customizations persist between sessions. A short walkthrough at the top of the page fires a demo Cheer event so you can try it.

---

## Alert queue controls

The **Controls** panel monitors and controls playback without leaving the page. Its header shows how many alerts are playing and queued.

Global controls: **Pause / Resume**, **Skip** (cut the current alert short on every queue), **Clear** (drop every queued alert), **Mute TTS / Unmute TTS**, and **Reload Overlays** (force every connected browser source to reload, which fixes a blank or errored overlay without touching OBS).

Expand the panel for per-queue rows showing the queue name, blocking or non-blocking status, assigned overlays and whether each is currently loaded in OBS, the playing alert, and the waiting count, with the same pause, skip, clear, and mute controls per queue.

Below the controls, live bars appear for hype trains, polls, predictions, and outgoing raids while they are running.
