# Dulcimer Chord Maps

**Chord shapes and tune walkthroughs for the hammered dulcimer.**

Dulcimer Chord Maps draws a hammered dulcimer as you see it from the player's seat and shows where things are on it. One tab maps chords: every place a triangle or shed shape fits for a chosen chord. The other walks through a tune note by note. It shows which hand strikes each note, where on the instrument to strike it, and where the next move goes. It can also build a backup part from the tune's chords.

It is one self-contained HTML file. Nothing needs to be installed or run, and it works in any current desktop or tablet browser.

Built by Steve Marsden (Stephen F. Austin State University) with Claude, while learning the instrument.

---

## Running it

Open `index.html` in a browser. To host it, place the file on any static web host, or turn on GitHub Pages for this repository (Settings → Pages → deploy from the `main` branch).

The page loads two typefaces from Google Fonts and the abcjs notation library from jsDelivr. Without a network connection, the map and walkthrough still work, with system fonts and without the drawn notation.

## The instrument

The map is set up for a **Cloud Nine 16/16**, tuned to the maker's chart:

| Bridge | Courses, front to back |
|---|---|
| Treble, right side | G♯3 A3 B3 C♯4 D4 E4 F♯4 G4 A4 B4 C5 D5 E5 F5 G5 G♯5 |
| Treble, left side | a fifth above the right side of the same course |
| Bass | A2 D3 E3 F♯3 G3 A3 B3 C4 D4 E4 F4 G4 A4 B♭4 C5 D♯5 |

Cloud Nine departs from the plain diatonic layout in a few places:

- The bass has F and B♭ in its upper half, which puts F major within reach.
- The treble has F5 where F♯5 would normally be.
- The top course on each bridge is a chromatic extra.

**Retune courses** lets a player correct any course to match a different instrument. The changes are kept in that browser.

## Chord map

Pick a key, then a chord from the key's numbered chords (I, ii, iii and so on) or any root and quality. Chord tones are colored by role: root, third, fifth, seventh. Two shapes can be outlined wherever they fit:

- **The triangle.** Root, the third two courses up on the same side, and the fifth straight across the bridge from the root. It works on the treble bridge and from the bass across to the right side of the treble.
- **The shed.** Root, third, fifth and octave, split between the hands. The right hand plays a third (the root and the course two up). The left hand plays a fourth (the fifth straight across from the root, and the octave three courses above it). It works across the valley between the bridges and across the treble bridge.

The same shape gives a major or a minor chord depending on where it starts. The map shows this directly instead of explaining it.

## Tune walkthrough

Tunes come in as [ABC notation](https://abcnotation.com/), the plain-text format most folk tune collections use. Paste a tune, load it, and step through it.

- **On the map:** the current note is filled in its hand's color (blue for right, amber for left). A plain ring shows where the other hand is waiting, and a dashed arrow shows the move to the next note.
- **On the score:** the current note is highlighted, R or L is printed under every note, and tapping a note jumps to it.
- **The hammering strip** lists every note with its hand, bar by bar, with the repeats written out. Each bar is labeled with its chords.
- **Transport:** step back and forward, or play at a set tempo. Any range of bars can be looped. The transport bar stays on screen while scrolling.

### How hands and spots are chosen

Most notes can be struck in two or three places. For each note, the page chooses the spot that keeps each hand's moves short and keeps the hands from crossing. It weighs the whole tune at once, using a Viterbi search over every possible placement. The result is a sensible first draft, not a rule. **Switch hand** and **Use the other spot** change any note, and the changes apply to both passes of a repeat.

Two alternation schemes are offered:

- **Count long notes** (the default) keeps both hands on the eighth-note pulse. A quarter note takes two strokes, the second one silent, so the lead hand always falls on the beat and both passes of a repeat are hammered the same way.
- **Every note played** alternates strictly.

The lead hand can be right or left. The whole tune can be moved up or down an octave when it doesn't fit the instrument.

### Backup

The **Backup** part follows chord symbols written in the ABC (`"G"`, `"D7"`, `"Em"`). When a tune has none, the page suggests a chord for each half bar from the melody notes. It favors the home chord and the chords on the fourth and fifth, and keeps a chord when the melody allows. Two styles are available:

- **Bass and chord:** a bass note on the beat with the right hand, and a two-note chord off the beat. Waltzes come out boom-chick-chick, and jigs get bass on the beat with the chord on the third eighth.
- **Shed rolls:** root, third, fifth and octave in running eighth notes.

The backup is placed and hammered by the same method as the melody, and every practice tool works on it.

### Harmony

**Harmony on the beats** adds a second note to each melody note that falls on a beat, struck with the other hand. The choices are a third below or above, a fifth below, a sixth below, or an octave below. The intervals follow the key, so thirds and sixths come out major or minor as the scale gives them.

### Practice tools

- **Trouble spots.** The page scores every move by distance against the time the hand has to make it. It also flags crossed hands and repeated strokes by one hand, and lists the worst bars in plain words. Tapping one loops that bar.
- **Hands-separate practice.** Right only or left only. Stepping skips to that hand's notes, and in playback the other hand's notes are played quietly or left out.
- **Click, count-in, and mute.** A metronome click on the beats, a count-in bar, and an option to mute the tune and play against the click alone.
- **Speed up each loop.** Raise the tempo by a set amount on each pass of a loop, up to a ceiling.
- **Chord shapes under the tune.** Outline the triangle and shed for the current chord near the hands.
- **My tunes.** Every loaded tune is kept in a list along with its hammering changes, in that browser.

## What the ABC reader handles

It handles the parts of ABC that ordinary fiddle tunes use:

- key signatures and modes, and accidentals that carry through the bar;
- note lengths, broken rhythm (`>` and `<`), triplets and other tuplets, and ties;
- rests;
- repeats and first and second endings, which are written out in order;
- pickup bars, which are counted from the end of the bar so the hands fall correctly;
- chord symbols in quotes.

Grace notes, decorations and ornaments are skipped. Where the music has a chord (`[GBd]`), the walkthrough takes its top note. Tunes written in more than one voice are not supported.

## Known limits

- **The placement is one reading.** Players and teachers hammer the same passage differently. The page aims for short moves and uncrossed hands, but not for every player's habits, such as keeping a run on one side of a bridge for its sound.
- **Suggested chords are suggestions.** They are worked out from the melody notes in each half bar. A few will be arguable, and chord symbols in the ABC override them.
- **The sound is synthesized.** It is close enough to check notes and timing, but it is not a recorded dulcimer, and it does not model dampers or sympathetic ringing.
- **No listening.** The page does not hear the player.

## Technical notes

- Everything is in a single `index.html`: inline CSS and JavaScript, with no build step. [abcjs](https://www.abcjs.net/) 6.4.4 draws the notation, and its note elements are mapped back to the walkthrough by character position.
- The tuning is two arrays near the top of the script, `DEF_T` (treble, right side) and `DEF_B` (bass), from the front of the instrument to the back. Changing those adapts the page to a different instrument.
- Placement is a dynamic-programming search over every candidate spot for every note. The state is the spots of the last two notes, which is enough to know where each hand is. The costs are hand travel, crossing, and a small preference for the treble in melodies.
- Playback schedules notes and clicks on the Web Audio clock a fifth of a second ahead, so timing holds steady at any tempo.
- The tuning, settings, and tune list are kept in `localStorage`. The page works the same without it.

## License

MIT. See [LICENSE](LICENSE).
