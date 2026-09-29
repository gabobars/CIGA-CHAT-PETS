# CIGA Chat Pets

A free, customizable **StreamElements chat pet widget for Twitch**.

CIGA Chat Pets turns your Twitch chat into a collection of animated pixel pets. When a viewer sends their first message, they receive their own pet that stays on screen, walks around the bottom of the overlay, displays their username, and can show their messages in a speech bubble.

The widget also includes an optional **Host Pet**, configurable colors, viewer tinting, custom movement behaviour, pixel fonts, entry animations, chat bubbles, persistent pet positions, and more.

No programming is required to use the widget. Everything is configured directly through **StreamElements Custom Fields**.

---

## Features

### Viewer Pets

Every viewer can receive their own pet when they send their first chat message.

Once a viewer has a pet, additional messages from the same viewer do not create another pet. Instead, the existing pet displays the new message in its speech bubble.

Viewer pets:

* Use the same configured sprite animation set.
* Have their own username displayed above them.
* Can use the viewer's Twitch username color.
* Can receive a deterministic color tint.
* Move around the bottom of the screen.
* Switch between idle and walking animations automatically.
* Can display chat messages in speech bubbles.
* Are limited by the configured maximum number of viewer pets.

The maximum number of viewer pets can be configured up to **20**.

The Host Pet does **not** count toward this limit.

---

## Host Pet

The widget includes an optional Host Pet.

The Host Pet can be enabled or disabled through:

`Enable Host Pet`

You can also configure:

* Host name
* Host name color
* Host speech lines
* Host speech timing
* Host bubble duration

The Host Pet uses the same animation assets as viewer pets, but does **not** receive viewer tinting.

The Host Pet can automatically display random lines at configurable intervals.

Example:

```text
Welcome to the stream!
I see you there...
Another viewer has arrived.
Interesting...
You were not supposed to find this place.
```

Multiple lines are separated using `|` in the `Host Lines` field:

```text
Welcome to the stream!|I see you there...|Interesting...
```

---

# Installation

## 1. Download the repository

Download or clone this repository.

The important files are located in:

```text
widget/
├── HTML
├── CSS
├── JS
└── Fields
```

These files correspond directly to the four sections of a StreamElements Custom Widget.

---

## 2. Create a StreamElements Custom Widget

Open your StreamElements dashboard and create a new Custom Widget.

The widget editor contains four main sections:

```text
HTML
CSS
JS
Fields
```

Copy the repository files into the corresponding sections.

Use:

```text
widget/HTML   → StreamElements HTML
widget/CSS    → StreamElements CSS
widget/JS     → StreamElements JS
widget/Fields → StreamElements Fields
```

Do **not** place `<script>` tags inside the JS section or create a separate HTML document around the code.

The StreamElements editor already provides the necessary widget environment.

---

## 3. Add your sprite assets

The widget requires two animation sets:

### Idle Frames

Choose the idle frames in the exact order they should be used:

```text
1 → 2 → 3 → 4 → 5 → 6
```

The widget automatically turns them into a ping-pong animation:

```text
1 → 2 → 3 → 4 → 5 → 6 → 5 → 4 → 3 → 2 → 1
```

### Walk Frames

Choose the walking frames in the exact order:

```text
1 → 2 → 3 → 4 → 5
```

The walking animation loops:

```text
1 → 2 → 3 → 4 → 5 → 1 → 2 →
```

