# Avatar Overlays

An avatar overlay is a character that talks when you talk, often called a PNGTuber. LuckyBot listens to your voice and swaps your pictures as you speak: mouth closed while you are quiet, mouth open while you talk, and a third picture when you shout if you have one. The character hops when you start talking and blinks on its own.

An avatar is also a [reactive overlay](reactive-overlays.md), so it can have an idle animation, Motion, and its own reaction for follows, subs, raids, and any other event.

<!-- shot: avatar-editor.png | /overlays/<avatar overlay>/alerts/<canvas> | an avatar open in the editor with two pictures added, the AVATAR bar above the canvas with Show set to Talking -->

---

## Creating one

Click **+ New Overlay**, open the **Avatar** tab, pick **Avatar**, name it, and click **Create**. Like a reactive overlay, it has a single canvas named **Canvas**; click it to open the editor.

---

## Adding your pictures

The **AVATAR** bar sits above the canvas. Click **Add pictures** to start.

<!-- shot: avatar-add-pictures.png | /overlays/<avatar overlay>/alerts/<canvas> | click Add pictures in the AVATAR bar, with the Not talking and Talking slots filled -->

A talking avatar needs two pictures: one with the mouth closed and one with it open. Two more are optional:

- **Not talking**: mouth closed. This is what shows most of the time.
- **Talking**: mouth open.
- **Shouting** (optional): shown when you get loud.
- **Blinking** (optional): the not-talking picture with the eyes closed.

Click a slot to choose a picture for it, or **From Media** to pick one from the [media library](media-library.md). **Choose pictures** takes several files at once and sorts them by the words in their names: a file named `fox_talk.png` goes to Talking, `fox_idle.png` to Not talking, `fox_shout.png` to Shouting, and `fox_blink.png` to Blinking. Files without one of those words fill the empty slots in order.

Use pictures with a transparent background, all the same size, so they line up. Click **Add to canvas** and each picture becomes a layer, already set to show at the right moment. Move and resize them like any other layer.

You can also build a character from separate parts, such as a body, a closed mouth, an open mouth, and eyes. Add them as layers with **+ Add** and set when each one shows (below).

---

## When each layer shows

Select a layer and open its **Animation** tab. The **Show when** section has two choices:

- **Mouth**: **Always**, **Not talking**, **Talking (any volume)**, **Talking, not shouting**, or **Shouting**.
- **Eyes**: **Always**, **Eyes open**, or **During a blink**.

A two-picture avatar uses **Not talking** on one layer and **Talking (any volume)** on the other. With a shouting picture, the talking layer uses **Talking, not shouting** so the two never show together. A layer left on **Always** for both stays on screen the whole time, which suits a body or a hat.

---

## Checking each state

The **Show** buttons in the AVATAR bar change what the canvas shows:

- **All layers**: every layer at once, for arranging them.
- **Not talking**, **Talking**, **Shouting**: the character as it will look in that state.
- **My voice**: the character runs from your voice, the same as on stream, with a level meter beside the buttons.

A layer hidden by the current state still shows, dimmed, while it is selected, so it can be edited.

---

## Voice settings

Click **Voice settings** in the AVATAR bar. Changes are kept when you click **Save** in the top bar.

<!-- shot: avatar-voice-settings.png | /overlays/<avatar overlay>/alerts/<canvas> | click Voice settings in the AVATAR bar, with the level meter showing -->

### Where the voice comes from

- **LuckyBot's microphone**: LuckyBot listens to a mic on this PC. Pick it under **Microphone**, or leave **System default**. This works without OBS. The LuckyBot app has to stay open.
- **An OBS audio source**: LuckyBot follows the level OBS shows for one source, after its filters, so a noise gate or suppression in OBS applies. Pick the source under **OBS source** and press **Refresh** if it is not listed. Muting the source in OBS closes the mouth. LuckyBot reaches OBS with the address and password saved on the [OBS page](stream-tools.md#obs).

LuckyBot only listens while an avatar overlay is open somewhere (in OBS or in the editor). If the voice stops arriving, for example because LuckyBot was closed, the mouth closes.

### Level

The meter shows your voice live, with a line for where talking starts and one for where shouting starts.

- **Talking starts at**: talk normally and set this just under where the bar sits. Room noise should stay to the left of it.
- **Shouting starts at**: where the shouting picture takes over. It never sits below the talking line.
- **Boost**: raises or lowers a quiet or loud source, from -20 to +20 dB.
- **Mouth movement**: **Opens and closes as you speak** follows each syllable, closing in the dips between them; a held sound keeps it open. **Stays open while you talk** keeps the mouth open for as long as you are talking, and **Mouth stays open** sets how long it waits through the gaps between words before closing.

### Movement

- **Hop when I start talking**: a small jump each time you start speaking, with a **Hop height** in pixels.
- **Blink**: the eyes close **About every** few seconds, with a little variety. Blinking only shows on layers set to **Eyes open** or **During a blink**.

Both are on for a new avatar and can be turned off. The reactive [Motion](reactive-overlays.md#motion-without-keyframes) behaviors (Bob, Sway, Breathe, Drift) work on top of them.

---

## Reactions

The ANIMATION bar, reactions, rules, sound per reaction, and **Test reaction** work exactly as on a [reactive overlay](reactive-overlays.md). A reaction plays while the character keeps talking, so a wave on a follow does not stop the mouth.

---

## In OBS

Click **Copy URL** in the editor (or on the overlay page) and add it as a browser source, like any other overlay.

An overlay inside OBS cannot open a microphone itself, so LuckyBot measures your voice and sends the level to it. Keep LuckyBot running while you stream.

---

## Troubleshooting

- **The mouth never opens.** Open **Voice settings** and talk: if the bar stays left of the talking line, lower **Talking starts at** or raise **Boost**. With an OBS source, check that the source is not muted in OBS and that LuckyBot can reach OBS.
- **The mouth flaps with background noise.** Raise **Talking starts at** until the room noise stays left of it, or use an OBS source with a noise gate on it.
- **"This browser cannot open a microphone on this address."** A dashboard opened from another PC on your network cannot use the microphone. Open LuckyBot itself on the streaming PC, or choose an OBS audio source.
- **Two pictures show at once.** Check each layer's **Show when**. With a shouting picture, the talking layer should be **Talking, not shouting**.
