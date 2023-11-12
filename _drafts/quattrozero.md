---
#layout: posts
permalink: /posts/QuattroZero/
title: "How I built my own Mechanical Keyboard from scratch"
categories: Posts
toc: true
toc_sticky: true

header:
  overlay_image: /assets/images/posts/40/endresult.jpg
  overlay_filter: 0.4
  caption: "QuattroZero looking goood!"
---

_In this new episode of **How I built my own thing from scratch** I decided to combine a lot of the good things I learned through my recent times and come up with something I could challenge myself and in the end have an object I could use every day. In this post, you will see how I combined 3D Design, 3D printing, laser cutting, soldering, coding, and much more to come up with this amazing result._
{: .notice--primary}

<p style="text-align:center;"><img src="{{ "/assets/images/posts/40/endresult-cropped.jpg" | absolute_url }}" width="100%" hspace="5"></p>

<i class="far fa-file-alt"></i> QuattroZero
{: .notice--info}
{: .text-justify}


_IMPORTANT: You will find my files and all you need to replicate my result through [this link][1]. If you go on building my version or some other make sure to contact me. I want to see your awesome mech keeb!_
{: .notice--primary}

## The Mech Keeb thing
Before deep diving into my project, I think it's a good idea to get ourselves on the same page.
So, what is a mechanical keyboard? The quick answer it's something like this: mechanical keyboards are an improved and better experience in comparison to your typical cheap office keyboard. Mech Keeb utilizes mechanical switches, tuned stabilizers, high-quality plastic for the keycaps, and much more intentionality in the typing experience. All of this is done to achieve the most pleasurable experience when typing.
Nowadays we are investing a lot of time sitting in front of a PC, therefore, I think it's a good idea to invest some time in high-quality gadgets like a keyboard and mouse to create a better environment while typing.
If all of this resonates with you I encouraged you to check the subreddit [r/MechanicalKeyboards][2] to take a look at the numerous alternatives there are in this world. Now let's get to the good stuff.

## My choices
For this project, I decided to go with a **hand-wired, stacked acrylic, tactile, ortho-linear 40% keyboard with PBT keycaps**. Let's break this down.
- **hand-wiring**: normal keyboards have a PCB (= circuit board) for controlling the electronics. I already learned about the process of creating a PCB in [this other post of mine][3], for this one I wanted to try this other method. It consists of creating a matrix with the wire through the switches and with the help of diodes and a small board like an Arduino you can substitute having to print a circuit.
- **stacked acrylic**: this is one of the numerous methods for creating a case for your keyboard. The goal is to use many layers of acrylic sheets (in my case I used plexiglass) to come up with a container for your other hardware. Just like 3D printing, but we are using 5 or 6 layers instead of hundreds.
- **tactile**: it refers to the switches, the mechanism that actuates the press of the key. There are linear, tactile, and clicky switches. For each of these three macroarea, there are an infinite amount of possibilities so you can choose the sound and feel you are looking for. I used a tactile switch: Akko CS Lavender Purple.
- **ortho-linear 40%**: this is infos about the layout. Ortholinear means that every key is positionated like in a matrix, everything is symmetrical and each key sits on top of the other. Normal keyboards have each row shifted by a bit. This comes from the early days of typewriters where each key mechanism needed space and therefore each key could not sit on top of each other. Nowadays there isn't this necessity anymore and the ortho layout should be more natural and comfortable to type on while touch typing. I'm eager to try this layout. 40% means a smaller format where some keys are missing. You can still type every character with the help of macros, shortcuts, and some software.
- **PBT keycaps**: to achieve a better sound and feel a better PBT plastic is used. Often a more thicker keycaps provide a better sound.

## The Story
Now it's time to illustrate my journey and how it all came to be.

### The Design

<p style="text-align:center;"><img src="{{ "/assets/images/posts/40/inventor.png" | absolute_url }}" width="80%" hspace="5"></p>

<i class="far fa-file-alt"></i> My 3D-model in Inventor.
{: .notice--info}
{: .text-justify}

I started in **AutoDesk Inventor**, my go-to 3D Design software. To create a stacked acrylic keyboard I thought in layers: the most important being the plate, at whom all the keys are fixed.
On the plate, I designed the cut-outs for the keys and stabilizers. I used [this datasheet][4] from Cherry MX to make sure I used all the right dimensions and tolerances. This is vital to achieve a working result.

<p style="text-align:center;"><img src="{{ "/assets/images/posts/40/plate.png" | absolute_url }}" width="80%" hspace="5"></p>

<i class="far fa-file-alt"></i> My sketch of the plate with its dimensions.
{: .notice--info}
{: .text-justify}

After the plate, I went down the layers and designed the other levels. I made sure I got a good way of bolting everything together with M3 bolts and nuts. I was quite happy with the result. It was also important, to make it look fancier, to have a cut-out for the USB C connection. I decided I would print a hub to make everything look good and tight.

<p style="text-align:center;"><img src="{{ "/assets/images/posts/40/bolts_nuts.png" | absolute_url }}" width="80%" hspace="5"></p>

<i class="far fa-file-alt"></i> My mounting concept: A nut in the middle and bolts at each side. I designed the cut-offs in the plexiglass to house the bolts.
{: .notice--info}
{: .text-justify}

### The Software
The firmware we are going to flash on our microcontroller is written in C and following some guidelines makes everything easier. You have to check out [QMK][5], an awesome open-source tool with a big and helpful community. You'll find numerous guides on how to create the perfect firmware for your keyboard.
The core file in every config looks something like this. This is my keymap.c file for my QuattroZero.
It looks intimidating but it's pretty simple. We are declaring different states and layers and explaining how they are constituted.

```
#include QMK_KEYBOARD_H

enum layers {
  _QWERTY,
  _LOWER,
  _RAISE,
  _ADJUST,
  _MOUSE,
  _NUM,
  _NUMMOD
};

#define LOWER MO(_LOWER)
#define RAISE MO(_RAISE)
#define NUM MO(_NUM)
#define NMOD MO(_NUMMOD)
#define MSCLN LT(_MOUSE,KC_SCLN)

const uint16_t PROGMEM keymaps[][MATRIX_ROWS][MATRIX_COLS] = {

[_QWERTY] = LAYOUT_ortho_4x12(
  KC_TAB,  KC_Q,    KC_W,    KC_E,    KC_R,    KC_T,    KC_Y,    KC_U,    KC_I,    KC_O,    KC_P,    KC_BSPC,
  KC_ESC,  KC_A,    KC_S,    KC_D,    KC_F,    KC_G,    KC_H,    KC_J,    KC_K,    KC_L,    MSCLN,   KC_QUOT,
  KC_LSFT, KC_Z,    KC_X,    KC_C,    KC_V,    KC_B,    KC_N,    KC_M,    KC_COMM, KC_DOT,  KC_SLSH, KC_ENT ,
  NUM,     KC_LCTL, KC_LALT, KC_LGUI, LOWER,   KC_SPC,  KC_SPC,  RAISE,   KC_LEFT, KC_DOWN, KC_UP,   KC_RGHT
),

[_LOWER] = LAYOUT_ortho_4x12(
  KC_TILD, KC_EXLM, KC_AT,   KC_HASH, KC_DLR,  KC_PERC, KC_CIRC, KC_AMPR,    KC_ASTR,    KC_LPRN, KC_RPRN, KC_BSPC,
  KC_DEL,  KC_F1,   KC_F2,   KC_F3,   KC_F4,   KC_F5,   KC_F6,   KC_UNDS,    KC_PLUS,    KC_LCBR, KC_RCBR, KC_PIPE,
  _______, KC_F7,   KC_F8,   KC_F9,   KC_F10,  KC_F11,  KC_F12,  S(KC_NUHS), S(KC_NUBS), KC_HOME, KC_END, KC_MPLY,
  _______, _______, _______, _______, _______, _______, _______, _______,    KC_MPRV,    KC_VOLD, KC_VOLU, KC_MNXT
),

[_RAISE] = LAYOUT_ortho_4x12(
  KC_GRV,  KC_1,    KC_2,    KC_3,    KC_4,    KC_5,    KC_6,    KC_7,    KC_8,    KC_9,    KC_0,    KC_BSPC,
  KC_DEL,  KC_F1,   KC_F2,   KC_F3,   KC_F4,   KC_F5,   KC_F6,   KC_MINS, KC_EQL,  KC_LBRC, KC_RBRC, KC_BSLS,
  _______, KC_F7,   KC_F8,   KC_F9,   KC_F10,  KC_F11,  KC_F12,  KC_NUHS, KC_NUBS, KC_PGUP, KC_PGDN, KC_MPLY,
  _______, _______, _______, _______, _______, _______, _______, _______, KC_MPRV, KC_VOLD, KC_VOLU, KC_MNXT
),

[_NUM] = LAYOUT_ortho_4x12(
  KC_CAPS, KC_PSCR, KC_SCROLL_LOCK, KC_PAUS,  _______, _______, _______, KC_P7,    KC_P8,    KC_P9,   _______, _______,
  _______, KC_INS,  KC_HOME,        KC_PGUP,  _______, _______, _______, KC_P4,    KC_P5,    KC_P6,   _______, _______,
  _______, KC_DEL,  KC_END,         KC_PGDN,  _______, _______, _______, KC_P1,    KC_P2,    KC_P3,   _______, _______,
  _______, NMOD,    _______,        _______,  _______, _______, _______, KC_P0,    KC_PDOT,  _______, _______, _______
),

[_NUMMOD] = LAYOUT_ortho_4x12(
  _______, _______, _______, _______, _______, _______, KC_NUM_LOCK, KC_PSLS,  KC_PAST,  KC_PMNS, _______, _______,
  _______, _______, _______, _______, _______, _______, _______,     _______,  _______,  KC_PPLS, _______, _______,
  _______, _______, _______, _______, _______, _______, _______,     _______,  _______,  KC_PENT, _______, _______,
  _______, _______, _______, _______, _______, _______, _______,     _______,  _______,  _______, _______, _______
),

[_MOUSE] = LAYOUT_ortho_4x12(
  _______, _______, KC_BTN1, KC_MS_U, KC_BTN3, KC_WH_U, _______, _______,  _______,  _______, _______, _______,
  _______, _______, KC_MS_L, KC_MS_D, KC_MS_R, KC_WH_D, _______, _______,  _______,  _______, _______, _______,
  _______, _______, _______, _______, _______, _______, _______, _______,  _______,  _______, _______, _______,
  _______, _______, _______, _______, _______, _______, _______,  _______,  _______, _______, _______, _______
),

[_ADJUST] = LAYOUT_ortho_4x12(
  QK_BOOT, DB_TOGG, _______, _______, _______,  _______, _______, _______, _______, _______, _______, _______ ,
  _______, _______, _______, _______, _______,  _______, _______, _______, _______, _______, _______, _______,
  _______, _______, _______, _______, _______,  _______, _______, _______, _______, _______, _______, _______,
  _______, _______, _______, _______, _______,  _______, _______, _______, _______, _______, _______, _______
)

};

layer_state_t layer_state_set_user(layer_state_t state) {
  return update_tri_layer_state(state, _LOWER, _RAISE, _ADJUST);
}

```

### The Manufacturing
The hands-on part. Let's begin!

#### Laser-Cutting
I created laser-cutting machine compatible files with the help of Inventor and proceeded to cut my layers. I learned it is vital to ensure a good quality cut that you make a lot of tests. I got the quality I needed with the help of some experienced friends - *Thanks Andrew! :)*

Look at this beauty! My logo's engraving is my favorite part.

<p style="text-align:center;"><img src="{{ "/assets/images/posts/40/laser1.jpg" | absolute_url }}" width="80%" hspace="5"></p>

<i class="far fa-file-alt"></i> Telling the laser machine what to do
{: .notice--info}
{: .text-justify}


<p style="text-align:center;"><img src="{{ "/assets/images/posts/40/laser2.jpg" | absolute_url }}" width="80%" hspace="5"></p>

<i class="far fa-file-alt"></i> The beast!
{: .notice--info}
{: .text-justify}


<p style="text-align:center;"><img src="{{ "/assets/images/posts/40/laser.jpg" | absolute_url }}" width="80%" hspace="5"></p>

<i class="far fa-file-alt"></i> The result
{: .notice--info}
{: .text-justify}


<p style="text-align:center;"><img src="{{ "/assets/images/posts/40/back.jpg" | absolute_url }}" width="100%" hspace="5"></p>

<i class="far fa-file-alt"></i> The back is engraved with this website's logo!
{: .notice--info}
{: .text-justify}


#### 3D Printing
After that, I exported from Inventor the .stl file for the USB C Hub and proceeded with the print in multiple colors to see which one was my favorite. I went with white.

<p style="text-align:center;"><img src="{{ "/assets/images/posts/40/usbc-hub.png" | absolute_url }}" width="80%" hspace="5"></p>

<i class="far fa-file-alt"></i> My USB-C hub in the Ultimaker Cura printing software
{: .notice--info}
{: .text-justify}

#### The soldering
This part was tough. A lot to solder. The goal is to wire up each row and column and feed these wires into the microcontroller.
With proper software, the microcontroller is able to identify the coordinates of the pressed key. To make sure there are no ghost clicks is important to have diodes paired with each key. This way current can flow only one way and we make sure that only one combination of row and column numbers corresponds to one key.



<p style="text-align:center;"><img src="{{ "/assets/images/posts/40/before-soldering.jpg" | absolute_url }}" width="80%" hspace="5"></p>

<i class="far fa-file-alt"></i> Before soldering - fit test
{: .notice--info}
{: .text-justify}



<p style="text-align:center;"><img src="{{ "/assets/images/posts/40/after-soldering.jpg" | absolute_url }}" width="80%" hspace="5"></p>

<i class="far fa-file-alt"></i> After soldering - it works!
{: .notice--info}
{: .text-justify}

### Building everything together
This is the fun part of every project: the moment everything comes together. It is so satisfying to see the result of what some (a lot) hours in the free time can lead to. This was my favorite project so far and I can't wait to iterate and make some perfections!

<p style="text-align:center;"><img src="{{ "/assets/images/posts/40/building-together.jpg" | absolute_url }}" width="100%" hspace="5"></p>

<i class="far fa-file-alt"></i> Ready to close the case
{: .notice--info}
{: .text-justify}


<p style="text-align:center;"><img src="{{ "/assets/images/posts/40/endresult-cropped.jpg" | absolute_url }}" width="100%" hspace="5"></p>

<i class="far fa-file-alt"></i> QuattroZero
{: .notice--info}
{: .text-justify}



<p style="text-align:center;"><img src="{{ "/assets/images/posts/40/other-view.jpg" | absolute_url }}" width="100%" hspace="5"></p>

<i class="far fa-file-alt"></i> QuattroZero
{: .notice--info}
{: .text-justify}


<p style="text-align:center;"><img src="{{ "/assets/images/posts/40/back.jpg" | absolute_url }}" width="100%" hspace="5"></p>

<i class="far fa-file-alt"></i> The back is engraved with this website's logo!
{: .notice--info}
{: .text-justify}

## The Files
Here can you find everything you'll need to complete your version of my design. Make sure to show me your results if you plan to do this yourself!

*Coming Soon*



<!-------------------------------- FOOTER --------------------------------->

[1]: https://LINK
[2]: https://www.reddit.com/r/MechanicalKeyboards/
[3]: https://www.matsan.it/posts/arduino-uno/
[4]: https://cdn.sparkfun.com/datasheets/Components/Switches/MX%20Series.pdf
[5]: https://docs.qmk.fm/#/
