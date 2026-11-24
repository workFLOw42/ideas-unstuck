# Part 2 — One system instead of five apps

> *"Smart isn't more gadgets. It's things working together."*

The problem from Part 1: lamps, speakers, a music subscription — and an app for each of them.
A big smart-home hub didn't fix it: it only knew two ways, **talk to it** or **tap an app**.
I wanted a **switch on the wall that just works** — for everyone in the family.

So: a Raspberry Pi at home running [Home Assistant](https://www.home-assistant.io), plus **real, physical,
smart wall switches**. No app needed, no voice commands needed.

## What's in this folder

| File | What it does | The lesson behind it |
|---|---|---|
| [`living_room_lights.yaml`](living_room_lights.yaml) | Wall relay, wall buttons, a dimmer dial and a TV light that adapts to the other lamps | **Two kinds of smart lamps:** bulbs behind a power-cutting relay need time to reconnect and only count as "on" with power — always-powered lamps just need a button. Plus a ping-pong lock against late "off" reports. |
| [`tv_after_dark.yaml`](tv_after_dark.yaml) | TV on after dark → TV light on, dimmed | **Sunset is too early** (≈ 27 min before civil dusk on the evening I measured). And: **what's already on, stays.** |
| [`nobody_home.yaml`](nobody_home.yaml) | Nobody home for 1 hour → lights off, music paused | Ask **"is anyone home?"**, not "is everyone away?" — and Wi-Fi presence isn't physical presence. |

**Placeholders:** every ID you have to fill in is in brackets — `[light_01]`, `[relay_01]`, `[speaker_01]`, `[tracker_01]`, `[scene_01]`, `[room_01]` …
Each file starts with a legend that says what goes where. Replace the placeholder **including the brackets**,
e.g. `light.[light_01]` → `light.living_room_ceiling`.

## Build it yourself

1. Install Home Assistant (a Raspberry Pi 4/5 or any small PC is enough) and add your lights and speakers
   through their integrations.
2. Create the scenes the examples use (`[scene_01]` … `[scene_05]`, see the legend in each file) in
   *Settings → Automations & Scenes → Scenes*.
3. Paste an example into *Settings → Automations → ⋮ → Edit in YAML*, replace all `[placeholders]`, save.
4. Test every path by hand: relay on/off, each button, the dial, TV on before and after dark.

## Build it with AI

Describe your **room**, not the code. For example:

> *"I use Home Assistant. In my living room, the ceiling has smart bulbs behind a smart wall relay that cuts
> the power. The dining lamp and the TV light are always powered and have wall buttons. Write one automation:
> the relay sets a ceiling scene once the bulbs are back online; the buttons toggle their lamps with a scene;
> a dial dims all lamps that are on in 5 % steps; and the TV light uses a brighter scene when both ceiling and
> dining lamp are on. Explain every step and tell me what could go wrong."*

Then **check it** — the last sentence of the prompt matters: ask what could go wrong, and test it at home.
Idea: human. Code: AI. Checked: human.

---
← [Part 1](../01-my-smart-home-wasnt-smart/) · Next: Part 3 — The first chip *(coming soon)*
