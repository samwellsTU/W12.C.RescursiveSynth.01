How We're Going to Make the `scaleMap` Function
===============================================

The `scaleMap` function is designed to take any MIDI note number and "snap" it down to the nearest note within a chosen scale. This is useful when you want to make sure all notes played conform to a scale like C Major or A Minor.

The Idea
--------

We’ll use a recursive approach to do this. Here’s how it works:

*   We take the input note and check if it's in the current scale.
*   If it is, we return it.
*   If it isn’t, we subtract 1 and try again—until we find a match.

Key Concepts
------------

*   **Modulo 12**: We use `noteIn % 12` to get the pitch class (e.g. C, C#, D...B), ignoring the octave.
*   **Recursion**: The function calls itself with `noteIn - 1` until it finds a scale match.

The Function
------------

    const scaleMap = function(noteIn) {
      // Check if note is in the scale (regardless of octave)
      if (currentScale.includes(noteIn % 12)) {
        return noteIn;
      } else {
        // Try the next note down
        return scaleMap(noteIn - 1);
      }
    };

Example
-------

If `currentScale = [0, 2, 4, 5, 7, 9, 11]` (C Major) and you pass in `62` (D), you'll get `62` back. If you pass in `63` (D#), it isn't in the scale, so the function calls itself again with `62`, then `61`, etc., until it finds a note that is in the scale.

Why This Is Cool
----------------

It’s a clean and flexible way to constrain incoming data (like random MIDI notes) to musical scales — without using loops! You could modify it later to go up instead of down, or even pick the closest note.