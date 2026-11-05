# NIS Keyboard

A small browser demo of the shoulder-surfing-resistant password entry idea from my paper, *Securing Graphical Password Techniques from Shoulder Surfing and Camera Based Attacks*.

The page has an on-screen keyboard (26 letters and 10 digits), a password field, and a JavaScript routine that encodes input with a Vernam (XOR) cipher against a randomly generated pad, then checks that decoding recovers the input.

## Run it

Open `index.html` in any browser. No build step, no dependencies.

`index.html` links to `Style.css`, which was not published with the paper's code listing, so the keyboard renders unstyled until you add your own stylesheet.

## Source

Kumar, E. (2022). *Securing Graphical Password Techniques from Shoulder Surfing and Camera Based Attacks.* International Journal of Recent Technology and Engineering (IJRTE), Vol. 11, Issue 3, September 2022. Published by BEIESP under CC BY-NC-ND 4.0.

https://www.ijrte.org/wp-content/uploads/papers/v11i3/B71640711222.pdf

The code is the listing from Section V of the paper. Changes from the printed listing:

- Re-indented for readability. No lines added, removed, or reordered.
- Replaced Greek look-alike letters with Latin ones in `charCodeAt`, the `SUBMIT` button label, the `A` and `B` key labels, and one comment. The Greek versions break the script.

## Known limitations of this listing

- `onkeydown="myFunction(event)"` passes the keyboard event, not the typed character. The event has no `.length`, so the encode loop never runs. Each keypress shows three alerts with a single random number, and the "decoding successful" check passes trivially because both sides are empty.
- The keyboard layout is static. The per-session layout randomization described in the paper is not implemented in this listing.
- The pad comes from `Math.random()`, which is not a cryptographically secure source. A production version would use `crypto.getRandomValues()`.
- `validateForm()` echoes the entered password back onto the page with `document.write`.

Treat this as a proof-of-concept sketch of the paper's idea, not a working security control.
