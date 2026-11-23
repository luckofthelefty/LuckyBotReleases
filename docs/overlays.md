# Overlays

An overlay is a browser page that runs inside OBS as a Browser Source. Each overlay has its own URL, its own content, and its own canvas size.

![Overlays page](images/overlays.png)
<!-- shot: overlays.png | /overlays | the Overlays page with a few cards showing their When and Shows chips, the share icon, and the Import, From a link and From StreamElements buttons -->



## Creating an overlay

Go to **Overlays** in the sidebar and click **+ New Overlay**. The New Overlay picker opens with seven tabs:

![Template browser](images/overlays-template-browser.png)
<!-- shot: overlays-template-browser.png | /overlays | click + New Overlay; show the seven tabs including Avatar, the Tour button in the header, Starter selected -->

- **Starter**: ready-made drop-ins. Stream Alerts is a full alert set (follow, sub, resub, gift sub, gift bomb, bits, raid); Charity Goal tracks a live Twitch charity campaign.
- **Basic**: event-driven alerts built in the drag-and-drop visual editor.
- **Static**: an always-on canvas for persistent graphics.
- **Widget**: always-on goals and live counters: follower, sub, and bits goals plus a multi-goal stack, all working with no other software. See [Widgets](widgets.md).
- **Reactive**: a character that reacts to events. An idle animation loops, and each event you add gets its own animation. See [Reactive Overlays](reactive-overlays.md).
- **Avatar**: a character that talks when you talk. Its mouth follows your voice, and it hops and blinks. See [Avatar Overlays](avatar-overlays.md).
- **Advanced**: the HTML/CSS/JS code sandbox, with templates like Spotify Now Playing, Twitch Polls, Twitch Predictions, Pipes, Weather, Sound Alerts, Subathon Timer, Thon Goals (Milestones), Up Next (Queue), a Custom WebSocket Feed, and Maze (WIP).

Pick a template, give the overlay a name, and click **Create**.

The captions overlay is not in the picker. It is made and styled on the Captions page, in its Overlay tab. See [Closed Captions](stream-tools.md#closed-captions).

### The New Overlay guide

The **Tour** button in the New Overlay header walks through the picker in about a minute: what each tab is for, picking a starting point, and naming it. If you read it to the end and then create an overlay, the guide carries on in the new overlay's page and finishes on getting it into OBS: which button copies the URL, and the width and height to give the Browser Source.

The guide starts by itself the first time someone with no overlays opens the picker. On the Overlays page, the **New to overlays?** card has a **Show me how** button that opens the picker with the guide already running. Each overlay's page and each editor also has its own **Tour** button.

---

## Overlay types

### Basic

Basic overlays use the visual alert editor. You add alerts to the overlay, each alert has layers (text, image, video, GIF, audio, shapes), and each layer has animation settings. See [Visual Editor](visual-editor.md).

### Static

A static overlay is a single always-on canvas built in the same visual editor, without alert events. Use it for frames, badges, and other persistent graphics.

### Widget

Widgets stay on screen and update live: goal bars, counters, and any Stats page number. See [Widgets](widgets.md).

### Reactive

A reactive overlay is an always-on canvas with a looping idle animation and one extra animation per event. A mascot that waves on a follow and jumps on a raid, for example. See [Reactive Overlays](reactive-overlays.md).

### Avatar

An avatar is a reactive overlay with a voice. You give it pictures for mouth closed and mouth open (plus shouting and blinking if you like), and it shows the right one as you speak. The voice comes from a microphone LuckyBot listens to, or from one OBS audio source. See [Avatar Overlays](avatar-overlays.md).

### Advanced

Advanced overlays give you a full code editor with HTML, CSS, JavaScript, and Fields tabs, plus a live preview. The `LUCKYBOT` JavaScript API is injected automatically (`BEACON` still works as an alias for older code):

```js
LUCKYBOT.on('Twitch.Follow', (data) => {
  // data contains the event payload
});
```

See [Advanced Editor](advanced-editor.md) for details.

---

## Managing overlays

The filter chips (All, Basic, Static, Widget, Advanced) narrow the list by type. Reactive and avatar overlays appear under All. Use the name filter, the sort (Recently updated or Name A-Z), and **Hide disabled** to tidy a long list. These choices are remembered.

Each overlay card shows the name, a type badge, the canvas size, and the overlay URL. Under them, a short summary reads like the rest of the app: **When** lists the events the overlay's alerts react to, and **Shows** counts its alerts and variants. Double-click the name to rename it inline. From the card you can:

- **Enable or disable** the overlay with the toggle. Disabled overlays serve a blank page and never play alerts.
- **Assign a queue** using the queue dropdown (basic and advanced overlays only). See [Alert Queues](queues.md).
- **Copy URL** for OBS, or **Preview** the overlay in a new browser tab.
- **Share with a link** with the share icon. See [Sharing with a link](#sharing-with-a-link).
- **Export** the overlay with the download icon.
- **Delete** the overlay with the trash icon. A pop-up names the overlay and asks "Are you sure you want to delete it?". It also warns that the overlay's alerts and settings go with it and that any OBS source using its link stops working. There is no undo for an overlay.

Click a card to open the overlay's page with its alert list. See [Alerts and Variants](alerts-and-variants.md).

---

## Importing from StreamElements

**From StreamElements** at the top of the page brings an existing StreamElements overlay into LuckyBot, media included.

![StreamElements import](images/overlays-import-se.png)

1. **Connect**: paste your StreamElements JWT (streamelements.com > Dashboard > Account > Channels, click Show secrets, copy the JWT Token). It stays on this computer and is only used to read your overlays. If you saved it under Settings > Connections > StreamElements, this step is skipped.
2. **Pick**: choose an overlay from your list, or paste an overlay URL or ID. The main AlertBox is not listed; open it in the StreamElements editor and paste its URL.
3. **Preview**: LuckyBot shows what it will create. Alert overlays become basic alerts with variants; custom widgets run under a StreamElements compatibility layer; image, video, and text layers compose into one overlay; label widgets bind to LuckyBot's live stats; goal widgets become native goal widgets you can restyle. Warnings list anything that cannot be carried over, such as custom code inside a basic alert (its media, text, and sound still import).
4. **Import**: media downloads into your library, overlays and alerts are created disabled. Review each one in the editor, then add its URL to OBS.

Chat bot commands and timers import separately, from the Chatbot page. See [Chatbot](chat-bot.md#import-from-another-bot).

---

## Sharing with a link

Any overlay can be shared with a link that installs it, images, sounds and video included, in someone else's LuckyBot. Share links go through LuckyBot Cloud:

- **Sharing** an overlay needs a paid LuckyBot Cloud subscription.
- **Installing** an overlay from a link needs LuckyBot connected to a cloud account. A free account is enough.

Connect the account in **Settings**, under **Connections**, **LuckyBot Cloud**.

<!-- shot: overlays-share.png | /overlays | click the share icon on an overlay card that is already shared; show the Share dialog with its link, Copy, Update link and Stop sharing -->

### Sharing an overlay

Click the share icon on the overlay's card, then **Create link**. LuckyBot packs the overlay with its media, uploads the copy, and gives you a link that looks like `https://cloud.luckybot.app/share/` followed by a long code. **Copy** it and send it to whoever should have the overlay. Keep LuckyBot open until the upload finishes.

- Only people you give the link to can get it. It is not listed anywhere.
- The link gives out the overlay as it was when you last uploaded it. Changes you make afterwards stay on your PC until you press **Update link**.
- **Stop sharing** turns the link off.
- The copy includes the overlay's settings. If you typed an API key or a password into one of its fields, clear it before sharing.

A shared overlay's share icon is highlighted on its card, and clicking it again opens the same dialog to copy, update, or stop the link. If your subscription ends, existing links keep working until you stop sharing them, but they can no longer be updated.

### Installing from a link

Click **From a link** at the top of the Overlays page, paste the link, and click **Look up**. LuckyBot shows the overlay's name, kind, size, and who shared it. **Download and review** downloads it and opens the normal import review, so you see what it is before anything is added. Opening a share link in your browser shows an **Open in LuckyBot** button, which opens this same dialog with the link filled in.

Only install overlays from people you trust. An Advanced overlay runs its own code, and the dialog says so.

---

## Exporting and importing

Overlays export as `.beacon` files you can move to another machine or send to someone.

### Exporting

Click the download icon on the overlay card. The export dialog lets you rename the export and shows who made it and on which version. **Include media files** bundles the images, videos, and audio into the file so the overlay works out of the box on any machine. Without it, the file is small but media has to be re-added after importing elsewhere.

### Importing

Click **Import** and pick a `.beacon` file, or drag and drop one anywhere on the page. Double-clicking a `.beacon` file in Windows also opens LuckyBot's import.

A confirmation shows the overlay name, type, and alert count before anything is created, and who shared it when it came from a share link. Advanced overlays show a security warning, since the file contains JavaScript that will run in your browser source. Only import files from sources you trust.

Bundles upload their media automatically, including files with less common extensions such as `.jfif` and `.oga`. Anything in a bundle that is not an image, sound, or video is left out. Plain files that reference media open a dialog after import so you can assign replacements from your media library. All imported alerts start disabled.

---

## Canvas size

The canvas size determines the dimensions of the overlay page. Set it to match your OBS browser source size so everything lines up.

Common sizes:
- 1920 x 1080 (standard 1080p)
- 2560 x 1440 (1440p)
- 1280 x 720 (720p)
- 1080 x 1920 (vertical)

Canvas size can be changed from the editor top bar.

---

## Missing media check

The first time you open the Overlays page after starting LuckyBot, it checks your overlays for broken media references (files that were moved or deleted). If any are found, a dialog lets you reassign them from the media library.

---

## Security notice

Every overlay page LuckyBot serves carries a Content Security Policy: only script LuckyBot wrote into the page may run. That closes the door on an attack where a crafted chat message becomes code inside an overlay that inserts viewer text as HTML.

If a page ever runs script from outside the policy, a **Security notice** badge appears on that overlay's card and a banner appears on Home. Click either for details: what tried to run, where, how many times, and when. If you did not add that code yourself and the overlay shows viewer text, treat it as an attack: disable the overlay, remove the code that inserts viewer text as HTML, and keep OBS on its latest version. If it is your own advanced code or an imported widget that uses inline handlers such as `onclick`, it is safe to **Dismiss notice**. The policy currently reports without blocking; LuckyBot's own runtimes never insert viewer text as HTML.

---

## Overlay open twice

When the same overlay URL is open in more than one place at once, LuckyBot shows an **Overlay open twice** banner on the Overlays page, and the overlay's card shows a **2 sources connected** badge. **Dismiss** hides the banner for those overlays; it comes back only if a different overlay is opened twice. Each alert still plays only once in the queue, but every copy plays its sound, so two unmuted copies are heard twice.

A second copy on purpose, such as one on an Aitum Vertical canvas, is fine: tick **Control audio via OBS** on that copy and mute it in the OBS mixer. If the copy is a leftover (often in another scene after re-creating a source), delete it. The badge clears within a few seconds of the extra page closing.
