# Advanced Editor

The advanced editor is a full HTML/CSS/JS code sandbox. Use it for overlays that need custom code, or start from one of the built-in advanced templates (Spotify Now Playing, Twitch Polls, Twitch Predictions, Pipes, Weather, Sound Alerts, Subathon Timer, Thon Goals, Up Next, Custom WebSocket Feed, Maze). The captions overlay is set up on the Captions page instead; see [Closed Captions](stream-tools.md#closed-captions).

![Advanced editor](images/advanced-editor.png)

---

## Layout

The top bar has **Copy URL** for OBS, **Preview** (opens the overlay in a browser tab), **Tour**, the canvas size, and **Save**. **Tour** walks through the preview, the settings, and the code, and ends on adding the overlay to OBS.

- **Left**: the code editor with tabs across the top.
- **Right**: a live preview of the overlay, with a **Settings** panel for the overlay's field values under it. Drag the divider to adjust the split.
- **Bottom**: a console panel for debugging. Drag its divider to resize.

---

## Code tabs

- **HTML**: the page markup.
- **CSS**: styles applied to the page.
- **JavaScript**: code that runs in the overlay.
- **Fields**: a JSON schema that defines configurable settings for the overlay.

The live preview updates shortly after you stop typing. Save with the **Save** button or Ctrl+S.

---

## The LUCKYBOT API

When your overlay loads, a `LUCKYBOT` global is injected automatically. `BEACON` is the same object, kept for older code.

```js
// Listen for a specific event
LUCKYBOT.on('Twitch.Follow', (data) => {
  console.log(data.user, 'followed');
});

// Listen for all events
LUCKYBOT.on('*', (type, data) => {
  console.log(type, data);
});
```

Event data is normalized across sources, so fields like `user`, `displayName`, `userId`, `amount`, and `tier` are consistent whether the event came from Twitch directly, Streamer.bot, or LuckyBot Cloud. Events arrive from the app's own Twitch connection first, then Streamer.bot, then Cloud, and duplicates of the same event are dropped.

Beyond events:

- `LUCKYBOT.config`: the overlay's own details (id, name, token, canvas size).
- `LUCKYBOT.fieldData`: the current values of your Fields.
- `LUCKYBOT.stats`: the live stats variables (session, totals, aggregates, labels, goals), updated by pushes. `LUCKYBOT.on('stats', ...)` fires on each update.
- `LUCKYBOT.store.get(key)` and `LUCKYBOT.store.set(key, value)`: a persistent key-value store shared by every overlay in your workspace. Writes reach the other overlays as a `kvstoreUpdate` event.
- `LUCKYBOT.sendChat(message)`: posts to your Twitch chat, limited to 60 lines a minute per overlay.
- `LUCKYBOT.chat(handler)`: raw chat messages as they arrive; call `.close()` on the returned stream to stop.
- `LUCKYBOT.currency.list()`, `.balance(viewer)`, `.add(viewer, amount)`, `.charge(viewer, amount)`, `.adjust(viewer, amount)`: read and move chatbot currency from an overlay, for games that pay out or charge an entry fee. `viewer` is a login, a numeric id, or a chat message. Every call takes an optional last argument, the slug of an extra currency from Chatbot > Currency; leave it out for the main currency. `charge` resolves `{ ok: false }` when the viewer cannot afford it.
- `LUCKYBOT.lumia`: Lumia Stream lights. See [Lumia lights](#lumia-lights).
- `LUCKYBOT.off(event, handler)`: stops a handler added with `LUCKYBOT.on`.
- `LUCKYBOT.on('fieldButton', d => ...)`: fires when a Button field is clicked in the Settings panel (`d.field` is the field key).

### Hype Train fields

Hype Train start, update, and end events carry who is driving the train as well as the numbers:

- `top_contributions`: the top cheerer and the top gifter, each with their user, type, and total.
- `is_shared_train` and `shared_train_participants`: whether the train is shared with other channels, and which ones.
- `is_treasure_train`, plus `all_time_high_level` and `all_time_high_total` when Twitch sends them.

These are the same names Streamer.bot uses, so an overlay reads them the same way whichever source delivered the event.

### Lumia lights

With Lumia Stream set up in **Connections > Lumia**, an overlay can run a Lumia command, Studio scene or animation, set a color, or fire a Lumia alert. Overlay lights use the same queue as the chatbot's Lumia steps: a burst from an overlay waits its turn with chatbot bursts, and a held redeem color comes back when it finishes.

```js
LUCKYBOT.lumia.command('red-alert', { behavior: 'burst', seconds: 30 });
LUCKYBOT.lumia.color('red 60', { behavior: 'burst', seconds: 10 });
LUCKYBOT.lumia.alert('twitch-bits', { username: 'coolfan', amount: 500 });
LUCKYBOT.lumia.stop();       // end this overlay's lights early
LUCKYBOT.lumia.toDefault();  // back to Lumia's default
```

- `behavior` is `'instant'` (the default), `'burst'` with `seconds` (plays for that long, then the held color or the default comes back), or `'hold'` with `minutes` (stays on for that long, through bursts).
- `command` also takes `type` for other kinds of Lumia command: `'chatbot-command'`, `'twitch-points'`, `'twitch-extension'`, `'studio-scene'`, `'studio-theme'`, or `'studio-animation'` (the default is a chat command). Add `message` for a command that reads one.
- `stop()` only ends this overlay's own lights. It never cuts off a chatbot light effect or a held redeem color. `toDefault()` returns to Lumia's default and clears every hold and queue.
- Every call resolves to `{ ok: true }` or `{ ok: false, error }`.

---

## Snippets

The **{ }** button (Code Snippets) beside the code editor opens ready-to-use examples. Click any snippet to insert it at the cursor. Snippets cover event listeners, reacting to a chat command, paying a viewer or charging an entry fee, Lumia lights, show and hide helpers, CSS animations, countdowns, and HTML structures such as an alert card.

A new blank overlay's JavaScript tab starts with a short list of the whole `LUCKYBOT` API as comments.

---

## Fields

The Fields tab defines settings that appear as form controls on the overlay's Settings panel, so things stay configurable without editing code. Use **+ Add Field** to build a field without writing JSON.

![Fields tab](images/advanced-editor-fields.png)

Supported field types:

| Type | Description |
|------|-------------|
| Text | Single-line text input |
| Textarea | Multi-line text input |
| Number | Number input (min, max, step) |
| Slider | Range slider |
| Checkbox | Boolean toggle |
| Color | Color swatch and hex input |
| Dropdown | Select from a list of options |
| Audio | Audio file from the media library, with volume, speed, pitch, start, and duration. **Test** plays it and turns into **Stop** while it plays |
| File | File path or media pick (image and video variants exist too) |
| Button | A button that sends a `fieldButton` event to the overlay |
| Hidden | Stored value readable from JavaScript, not shown |

Fields can be grouped into collapsible sections with the `group` property. In your HTML and CSS, `{{fieldKey}}` references a field's value and is replaced when the overlay renders.

---

## Template updates

Overlays created from a built-in template remember which one. When a LuckyBot update improves that template, an **Update template** button appears in the editor. Clicking it replaces the overlay's code with the latest version while keeping your field values. Manual code edits are overwritten, so skip the update if you have customized the code.

---

## Console

The console panel captures `console.log`, `console.error`, and other output from the preview, with an error count in its header. Type expressions into the console input to run them against the live preview. Check **Test Live** to also run typed snippets in every connected browser source, which is useful for debugging the overlay as it runs in OBS.

Uncaught errors and `console.error` lines from the live pages in OBS are also written to the app's server log, so they end up in a bug report bundle.

---

## Canvas size

Use the canvas size control in the top bar to pick a preset or enter custom dimensions. Changes apply immediately.
