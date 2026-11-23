# Home Assistant

Connect your own [Home Assistant](https://www.home-assistant.io) and your stream can run your lights, scenes, scripts, and other devices: a raid turns the room red, a cheer flashes the desk lamp, a viewer types `!lights blue`. LuckyBot talks to Home Assistant directly on your network.

The **Home Assistant** page is in the sidebar under Live. It has four tabs: **Home**, **Automations**, **Devices**, and **Connection**.

<!-- shot: home-assistant-home.png | /home-assistant | Home tab with room chips, device tiles, and the Scenes and Scripts panels; use a test setup with made-up room and device names -->

---

## Connecting

Open the **Connection** tab (the same settings are under **Settings > Connections > Home Assistant**).

1. Type the **Address** you open Home Assistant at in a browser, for example `http://homeassistant.local:8123`, or click **Find on my network** and pick it from the list.
2. Click **Sign in with Home Assistant**. Home Assistant's login page opens in your browser. Log in and approve LuckyBot; the page updates by itself.
3. If you would rather use a token, click **Or paste a long-lived access token**. In Home Assistant, click your name at the bottom left, open the Security tab, scroll to Long-lived access tokens, click **Create token**, and name it LuckyBot. Paste it and click **Save and test**.

The status line names the Home Assistant it reached and its version. The token is stored on this PC and never shown again. Once connected, Home Assistant also appears in the status strip at the top of Home.

---

## Home

Your devices as tiles, grouped by room, with a chip per room and **All rooms**. Click a tile to switch it on or off. A light that dims or changes color has an adjust button for brightness, eight color swatches, and Warm, Neutral, and Daylight whites. Scenes and scripts sit in their own panels on the side; click one to run it.

The page refreshes every few seconds while it is open, so changes made elsewhere show up.

---

## Automations

Everything in LuckyBot that controls Home Assistant, as When / Only if / Do cards, grouped into **Stream events**, **Chat commands and rewards**, **Walk ons**, and **Timers**. They are regular chatbot commands, timers, and walk ons, so **Edit** opens the same editor as the [Chatbot](chat-bot.md) page.

**+ New automation** starts a command with a Home Assistant step that runs on events only: pick the event (a raid, a sub, a cheer) under When.

---

## Devices

Every device LuckyBot can control, with a search box and a filter per kind (Lights, Switches, Scenes, and so on). Two switches per device:

- **Show on Home**: whether it gets a tile on the Home tab. Lights, scenes, scripts, and fans show by default.
- **Viewers can control**: whether a viewer's typed value may pick this device (see below).

---

## The Home Assistant step

Commands, timers, and walk ons have a **Home Assistant** step. Pick what it does:

- **Turn on**, **Turn off**, or **Toggle** any device. Turning on a light also takes a **Color** (a name like red, a hex code like `#ff8800`, or a white like `3000k`) and a **Brightness %**.
- **Run a scene**, **Run a script**, or **Press a button**.
- **Call a service (advanced)**: any Home Assistant service, such as `light.turn_on`, with optional JSON data.

Then pick the device: start typing and the box suggests your real devices by name, filtered to the ones that action fits. **Refresh devices** loads the list again.

Turn on, Turn off, and Toggle can **Put it back the way it was after** a number of seconds, so a flash of red returns the lamp to its old color and brightness. Leave it at 0 to leave the device as the step set it.

Fields take values like any other step. `$(1)` in the Color field lets a viewer pick the color: a command `!lights` with a Turn on step, the device `light.desk_lamp`, and Color `$(1)` turns the lamp blue on `!lights blue`. See [Commands](commands.md) for values and the rest of the steps.

### What viewers may control

When the device itself comes from a value a viewer types, like `!light $(1)`, the step only runs if that device is switched on under **Viewers can control** on the Devices tab. Locks, alarms, covers (garage doors and blinds), cameras, valves, and sirens can never be picked that way. A custom service step cannot take its device or target from a typed value at all.

A step that names its device directly is not limited by this, so a raid can always turn on the scene you chose.

---

## On the Activity feed

When an event runs a command with a Home Assistant step, the [Activity feed](activity-feed.md) shows it as a chip under that event, so you can see which event set off which lights.
