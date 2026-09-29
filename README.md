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
1 → 2 → 3 → 4 → 5 → 1 → 2 → ...
```

The widget preloads the animation assets when it starts.

Frames are not requested from the server every time the animation changes.

---

# Configuration

All configuration is available through StreamElements Custom Fields.

The settings are grouped to make the widget easier to configure.

---

## 01 // PET ASSETS

### Idle Frames

The animation frames used while a pet is standing still.

Recommended:

```text
6 frames
```

The widget automatically creates the ping-pong sequence.

### Walk Frames

The animation frames used while a pet is walking.

Recommended:

```text
5 frames
```

Make sure the frames are selected in animation order.

---

# 02 // TEXT

### Pixel Font

The font used for usernames and chat bubbles.

The default font is:

```text
Silkscreen
```

You can replace it with another supported Google Font.

---

# 03 // PET

### Pet Size (px)

The base size of the pet in pixels.

Default:

```text
120
```

This controls the size of the pet container before sprite scaling.

### Sprite Scale

Additional scaling applied to the sprite.

Default:

```text
1.40
```

This allows you to make the actual character larger or smaller without changing the base pet size.

### Ground Offset (px)

Controls how far the pet is moved vertically from the bottom of the overlay.

Default:

```text
0
```

Conceptually:

```text
0     = sprite touches the ground
-1    = slightly lower
-10   = more embedded into the ground
+10   = slightly above the ground
```

This is particularly useful when the character artwork contains transparent space below the feet.

### Maximum Viewer Pets

The maximum number of viewer pets that can exist at the same time.

Default:

```text
20
```

The maximum allowed value is 20.

The Host Pet does not count toward this limit.

### Base Frames Face Right

Tells the widget which direction the original sprite frames face.

If the original assets face right:

```text
ON
```

If the original assets face left:

```text
OFF
```

The widget automatically flips the sprite when necessary so the character faces the direction it is walking.

### Frame Duration (ms)

Controls the duration of each animation frame.

Lower values:

```text
faster animation
```

Higher values:

```text
slower animation
```

---

# 04 // MOVEMENT

### Idle Minimum

Minimum amount of time the pet stays idle.

### Idle Maximum

Maximum amount of time the pet stays idle.

The actual duration is randomized between the configured limits.

Idle durations are snapped to complete animation cycles so the pet does not randomly stop halfway through its idle animation.

### Walk Minimum

Minimum walking duration.

### Walk Maximum

Maximum walking duration.

Walking duration is also randomized and snapped to complete walking animation cycles.

### Minimum Walk Distance (%)

Minimum percentage of the usable screen width that a pet should attempt to walk.

### Maximum Walk Distance (%)

Maximum percentage of the usable screen width that a pet should attempt to walk.

### Screen Margin (%)

Keeps pets away from the extreme edges of the overlay.

For example:

```text
5%
```

means the pet will keep approximately 5% of the usable width as a margin.

---

# 05 // ENTRY

### Entry Effect

Controls whether newly created pets use the entry animation.

When enabled, a new pet appears with a small pop/bounce effect.

The animation uses no additional sprite frames.

### Entry Duration (ms)

Controls how long the entry animation lasts.

---

# 06 // CHAT

### Show Message Bubble

Controls whether pets display chat messages in speech bubbles.

### Message Duration (sec)

How long a viewer message stays visible.

### Maximum Message Characters

Maximum number of characters displayed from a chat message.

Longer messages are automatically truncated.

### Bubble Maximum Width (px)

Maximum width of a message bubble.

Long messages automatically wrap onto multiple lines.

### Bubble Font Minimum

Smallest font size the widget may use for long messages.

### Bubble Font Maximum

Largest font size used for short messages.

The widget automatically reduces the font size as messages become longer.

---

# 07 // USERNAME

### Username Font Size

Controls the size of the username displayed above each pet.

### Maximum Username Characters

Limits the username length.

Long usernames are automatically shortened with:

```text
…
```

Example:

```text
VeryLongViewerNameHere
```

may become:

```text
VeryLongViewer…
```

### Use Twitch Username Color

When enabled, the widget attempts to use the viewer's Twitch chat username color.

If a usable Twitch color is not available, the configured fallback color is used.

### Fallback Username Color

The username color used when a Twitch username color is unavailable or disabled.

### Fallback Username Outline

Fallback outline color used around usernames.

The widget also automatically chooses a contrasting outline for readable username text when possible.

This helps darker Twitch colors remain visible.

---

# 08 // BUBBLE

### Bubble Background

Background color of chat bubbles.

### Bubble Border

Border color of chat bubbles.

The speech bubble includes a small triangular pointer pointing toward the pet.

---

# 09 // VIEWER TINT

Viewer tint is designed to behave like a **transparent colored lens placed over the character**, rather than replacing the character's original colors.

The original sprite remains visible underneath the tint.

### Enable Viewer Tint

Enables or disables viewer tinting.

### Tint Intensity

Controls the strength of the tint.

Lower values:

```text
more original sprite color
```

Higher values:

```text
stronger color wash
```

The default is:

```text
0.28
```

### Tint 1 → Tint 6

Six configurable tint colors are available.

Each viewer is assigned a tint automatically.

The assignment is deterministic and tied to the viewer's identity.

The system also attempts to avoid assigning the same tint to multiple active viewers.

This means the first six active viewers can use different tint colors.

Once more than six viewers are active, tint colors may need to be reused.

The Host Pet does not receive a viewer tint.

---

# 10 // HOST

### Enable Host Pet

Enables or disables the Host Pet.

### Host Name

The name displayed above the Host Pet.

### Host Name Color

Controls the Host Pet username color.

### Host Lines

Lines spoken by the Host Pet.

Separate each line using:

```text
|
```

Example:

```text
Welcome to the stream!|Interesting...|I see you there.|Another viewer has arrived.
```

The widget randomly selects one of the configured lines each time the Host speaks.

### Host Speech Minimum Delay (sec)

Minimum amount of time between Host messages.

### Host Speech Maximum Delay (sec)

Maximum amount of time between Host messages.

The actual delay is randomized between the configured limits.

### Host Bubble Duration (sec)

Controls how long the Host's message bubble remains visible.

---

# 11 // OTHER

### Ignore Streamer Messages

When enabled, messages sent by the streamer account are ignored for viewer pet creation.

This is useful when using the Host Pet separately from the streamer's own chat messages.

---

# How Viewer Pets Work

The first time a viewer sends a valid chat message:

```text
Viewer sends message
        ↓
Widget identifies viewer
        ↓
No existing pet found
        ↓
New pet is created
        ↓
Entry animation plays
        ↓
First message appears in bubble
```

When the same viewer sends another message:

```text
Viewer sends message
        ↓
Existing pet found
        ↓
No new pet is created
        ↓
Existing pet displays the new message
```

This means a viewer does not create a new pet every time they chat.

---

# Pet Movement

Pets alternate between two states:

```text
IDLE
 ↓
WALK
 ↓
IDLE
 ↓
WALK
 ↓
...
```

While idle, the pet remains in its current horizontal position.

While walking, the pet smoothly travels to a randomly selected location within the configured movement limits.

Movement and animation are handled independently, allowing the walking frames to begin at the same time as the movement.

The widget does not rely on per-frame network requests or repeated asset downloads.

---

# Pet Positioning

Pets are positioned relative to the bottom of the overlay.

The horizontal position is represented by the center of the sprite.

The widget automatically calculates safe movement bounds based on:

* overlay width
* pet size
* sprite scale
* screen margin

This prevents the pet from walking too far outside the visible area.

---

# Entry and Leave Animations

New pets can use the configured entry animation.

The entry animation is a small:

```text
fade + pop + bounce
```

effect.

No extra sprite frames are required.

The widget also supports a leave animation using the same movement in reverse:

```text
ENTRY

fade in
  +
pop upward
  +
scale up
```

reversed into:

```text
LEAVE

scale down
  +
move downward
  +
fade out
```

The leave animation is used when the Host Pet is disabled while the widget is handling the corresponding configuration change.

---

# Configuration Changes

### Important

StreamElements may reinitialize the widget when configuration changes are made.

Because of this, it is strongly recommended to finish configuring the widget **before using it during a live stream**.

Changing settings such as:

* Host name
* Host size
* Sprite scale
* Movement settings
* Bubble settings
* Font settings
* Tint settings
* Host enable/disable

can cause the widget to be recreated.

Depending on how StreamElements or OBS reloads the widget, existing pets may be recreated as part of that process.

The Host Pet may also return to its starting position when the widget is fully recreated.

For this reason, avoid changing production settings during a live broadcast unless necessary.

---

# Saving Changes in StreamElements

After changing the widget configuration:

### 1. Save the widget in StreamElements

Use the StreamElements **Save** button.

### 2. Refresh the widget source in OBS

Refresh the browser source containing Chat Pets.

This ensures OBS loads the latest version of the widget and its configuration.

Do not assume that changing a Field automatically means the existing OBS browser source has fully refreshed.

---

# Refresh and Pet State

The widget maintains temporary pet state so pets can survive certain widget reinitializations and reload situations.

Stored information can include:

* viewer identity
* username
* username color
* horizontal position
* facing direction
* tint assignment

This allows restored pets to return to approximately the same position instead of being treated as completely new viewers.

Restored pets do not receive the new-pet entry animation.

---

# Reset Behaviour

A complete widget reset clears the current pet state.

This removes:

```text
all viewer pets
+
the Host Pet
```

The next viewer message will create a completely new pet.

The reset behaviour is intentionally not exposed as a normal public configuration option.

When testing or making major configuration changes, expect a full reset/recreation of the widget to start the pet state again.

---

# Important Limitations

## Maximum of 20 viewer pets

The widget supports up to 20 viewer pets at once.

If more viewers join after the limit is reached, older viewer pets may be removed to make room for new ones.

The Host Pet is separate from this limit.

---

## Six tint colors

There are six configurable tint slots.

The widget can avoid tint duplication while there are up to six active viewer pets.

With more than six active viewers, tint colors must eventually be reused.

---

## All viewers use the same sprite set

The current public version uses one configured set of:

```text
Idle Frames
+
Walk Frames
```

for all viewers.

Each viewer is differentiated through username, color, and optional tint.

---

## Sprite artwork is not included

The repository provides the widget code and configuration structure.

You must provide your own compatible sprite assets through the StreamElements image fields.

Make sure the frame order matches the intended animation order.

---

## Pixel-art recommendations

For the best results:

* Use PNG images with transparency.
* Keep all frames at the same dimensions.
* Keep the character aligned consistently between frames.
* Keep the character's feet at approximately the same vertical position.
* Avoid unnecessary transparent padding differences between frames.
* Make sure all idle frames use the same facing direction.
* Make sure all walk frames use the same facing direction.

Inconsistent frame dimensions or positioning can cause the character to appear to move or jump during animation.

---

# Recommended Asset Setup

A typical setup looks like this:

```text
Idle:

idle_1.png
idle_2.png
idle_3.png
idle_4.png
idle_5.png
idle_6.png


Walk:

walk_1.png
walk_2.png
walk_3.png
walk_4.png
walk_5.png
```

Select them in exactly that order in StreamElements.

---

# Recommended Starting Settings

The default configuration is intended as a general starting point.

```text
Pet Size:                  120
Sprite Scale:              1.40

Frame Duration:            120 ms

Idle Minimum:              1.8 sec
Idle Maximum:              4.2 sec

Walk Minimum:              2.4 sec
Walk Maximum:              5.8 sec

Minimum Walk Distance:     15%
Maximum Walk Distance:     50%

Screen Margin:             5%

Entry Effect:              ON
Entry Duration:            280 ms

Message Bubble:            ON
Message Duration:          4.2 sec

Maximum Message Characters: 90

Username Font Size:        18
Maximum Username Characters: 18

Viewer Tint:               ON
Tint Intensity:            0.28

Host Pet:                  ON
```

These values are only a starting point. The correct configuration depends on your sprite artwork, overlay layout, and stream resolution.

---

# OBS Setup

Once the widget is configured in StreamElements:

1. Add the StreamElements overlay/browser source to OBS.
2. Position it over your stream layout.
3. Make sure the source has transparency enabled through the widget itself.
4. Use the same overlay dimensions as your stream whenever possible.
5. After changing widget settings, save the StreamElements widget and refresh the source in OBS.

The widget is designed to work as a transparent overlay, so it can be placed over gameplay, VTuber layouts, PNGtuber scenes, webcams, backgrounds, or other stream elements.

---

# Troubleshooting

## Pets are not appearing

Check that:

* The widget is receiving Twitch chat events.
* The JS and Fields were copied correctly.
* Idle and Walk assets were selected.
* The StreamElements widget was saved.
* The OBS browser source has been refreshed.

---

## The pet is stuck in Idle

Check the Walk Frames field.

If no valid walk frames were loaded, there is no walking animation available.

The widget logs asset loading information to the browser console.

Look for:

```text
Chat Pets // assets loaded
```

and verify that `walkFrames` is greater than zero.

---

## The pet faces the wrong direction

Check:

```text
Base Frames Face Right
```

Enable it when your source frames face right.

Disable it when your source frames face left.

---

## The sprite appears too high or too low

Adjust:

```text
Ground Offset
```

A small negative value can help sprites with extra transparent space underneath them sit correctly on the ground.

---

## The username is difficult to read

The widget automatically attempts to select a contrasting outline based on the username color.

You can also adjust:

```text
Username Font Size
Fallback Username Outline
```

---

## Tint looks too strong

Lower:

```text
Tint Intensity
```

For example:

```text
0.20
```

will preserve more of the original sprite colors than:

```text
0.50
```

The tint is intended to act as a translucent color wash rather than completely recoloring the sprite.

---

## Changes are not appearing in OBS

Make sure you:

```text
1. Change the settings
2. Save in StreamElements
3. Refresh the Chat Pets browser source in OBS
```

---

# Repository Structure

```text
CIGA-CHAT-PETS/
│
├── README.md
├── LICENSE
│
├── widget/
│   ├── HTML
│   ├── CSS
│   ├── JS
│   └── Fields
│
└── preview/
    └── preview.png
```

The files inside `widget/` are designed specifically for the StreamElements Custom Widget editor.

---

# License

CIGA Chat Pets is released under the **MIT License**.

See [`LICENSE`](LICENSE) for the full license text.

The MIT License applies to the project code.

Sprite artwork and other assets are not automatically covered by the code license unless explicitly stated by their respective creators.

---

# Credits

Created by **CIGA**.

CIGA Chat Pets is provided as a free community widget for Twitch and StreamElements.

---

# Support

Before reporting a problem, make sure you are using the latest version from this repository and that the StreamElements widget contains the current HTML, CSS, JS, and Fields files.

When reporting an issue, include:

* browser/OBS version
* StreamElements setup
* the relevant widget settings
* a description of what happened
* console errors, if any
* screenshots or recordings when useful

This makes reproducing the issue much easier.
