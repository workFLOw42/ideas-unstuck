# Part 3 — The first chip

> *"Every thing can be a story figure."*

My son wanted his own music and audiobooks — no phone, no tablet, no pricey music box with figures that
cost extra every time. But the **speakers** and the **music subscription** were already there.

So: a small open-source **NFC reader** next to his speaker, and **every chip gets its own playlist**.
Put a chip on the reader, the music starts — on his own speaker. The chip can be anything:
a sticker, a card, a toy brick.

## The reader

I didn't design the reader — I used **[adonno/tagreader](https://github.com/adonno/tagreader)**, an open-source
NFC reader for Home Assistant, built with [ESPHome](https://esphome.io). Thank you, adonno!

| Part | What it does |
|---|---|
| ESP8266 board (Wemos D1 mini) | Wi-Fi, talks to Home Assistant |
| PN532 NFC module (I²C) | reads the chips (NTAG stickers, cards …) |
| one RGB LED (WS2812) | shows that something happened |
| a small buzzer | beeps when a chip was read |

Flash the ESPHome config from the tagreader repo, add the device in Home Assistant — every chip you put on
it now fires a `tag_scanned` event, and shows up in *Settings → Tags*.

**One lesson from a tag that stays on the reader:** the reader keeps seeing it over and over. Remember the
last chip and ignore it until it is taken off — that saves the small ESP8266 a lot of work over hours.

## What's in this folder

| File | What it does | The lesson behind it |
|---|---|---|
| [`chip_plays_playlist.yaml`](chip_plays_playlist.yaml) | Chip scanned → look it up in one list → play it on the speaker in that room | Recognise the reader by its **name**, not its `device_id` (that one changes when a device is re-added — and then nothing happens, without any error). **One list** for all chips. **Unknown chip → log it**, don't guess. |

**Placeholders:** `[reader_name_01]`, `[speaker_01]`, `[tag_id_01]`, `[playlist_uri_01]` … — the legend at the
top of the file says what goes where. Replace them **including the brackets**.

## Build it yourself

1. Build the reader (see [adonno/tagreader](https://github.com/adonno/tagreader)) and add it to Home Assistant.
2. Put each chip on the reader once. It appears in *Settings → Tags* — copy its ID.
3. Paste the example into *Settings → Automations → ⋮ → Edit in YAML*, fill in the reader name, the speaker
   and one line per chip.
4. Test: known chip → music on the right speaker. Unknown chip → a warning in *Settings → System → Logs*.

## Build it with AI

Describe the **situation**, not the code. For example:

> *"I use Home Assistant. Next to my son's speaker there is an ESPHome NFC reader that fires tag_scanned.
> Write one automation: when a chip is scanned on this reader, look up the tag ID in a list inside the
> automation and play the matching playlist on his speaker. Recognise the reader by its device name, not
> the device_id. Unknown chips should only write a warning to the log. Explain every step and tell me what
> could go wrong."*

Then **check it** — and test it with a known and an unknown chip.
Idea: human. Code: AI. Checked: human.

## And then?

He loved it. For a while. Then every new album meant a new chip — fifty albums, fifty chips.
There had to be a lazier way …

---
← [Part 2](../02-one-system-instead-of-five-apps/) · Next: Part 4 — The randomizer *(coming soon)*
