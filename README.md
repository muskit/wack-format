# 🏗 UNDER CONSTRUCTION
Currently in early stage. Details like package topology and .mer tags may change! Check commit history to see what's changed.

# Topology
**A song is packaged as a folder**. Songs can be nested in subfolders for organization purposes. However, a single file -- `meta.mer` -- must be present to define its folder as a song (detailed later).

To represent a song as a single file, that folder can be placed in a zip file with the extension `.wack`. Such files may contain multiple songs, also nested in subfolders.

## Song Folder Contents
```
<any name>/
├─ 0.mer // numbered charts
├─ 1.mer
├─ 2.mer
├─ 3.mer
├─ meta.mer // song metadata
├─ jacket.png/.jpg
├─ *.mp3/.ogg/.wav //SONG AUDIO
```

# .mer Files
There are two types of .mer files in a song: *metadata* and *charts*. Both types are detailed in the following subsections.

> [!WARNING]
> For any .mer file, **tags not defined here may be added**. Please keep this in mind when consuming.

## meta.mer
**This file must be present to define its folder as a song.**

Everything here only dictates how the song is displayed in song select; none of these tags affect gameplay in any of the song's charts.

### Tags
- `#TITLE` str
- `#RUBI_TITLE` str?
  - alternate representation of song title for sorting with Japanese kanji/kana
  - can only include alphanumeric, full-width alphanumeric, and katakana characters
- `#ARTIST` str
- `#RUBI_ARTIST` str?
  - same as `RUBI_TITLE`, but for the song's artist
- `#COPYRIGHT` str?
  - a carry-over from WACCA; can be used for sub-text not related to copyright.
- `#GENRE` str?
  - a carry-over from WACCA; can be used for arbitrary sorting purposes (**DELIBERATION NEEDED**)
- `#BPM` str
  - **does not actually affect gameplay tempo**; that's defined in charting!

*`?` = tag is optional

## Chart .mer
- **There can only be four charts in a song.**
- **The chart's filename must contain contain a positive number that may be padded.** The difficulty sorting of charts is determined by the first positive number found in the filename, and the named difficulty is assigned in this order:
  ```
  1. Normal
  2. Hard
  3. Expert
  4. Inferno
  ```
  - This means that, if you want, you can put the difficulty level of a song in the filename and it should be sorted in song select accordingly. For example:
    - `6.mer` will be set as Normal
    - `9p.mer` will be set as Hard
    - `11.mer` will be set as Expert
    - `13p.mer` will be set as Inferno
  - Tied numbers will be sorted by filenames' alphabetical value
  - If you would like to make a lower-difficulty chart have a higher level, you can number it accordingly in the filename for sorting.

### Tags
- `#LEVEL` float
- `#AUDIO` str
  - name of audio file containing music for this chart
- `#OFFSET` float
- `#CLEAR_THRESHOLD` float
  - WACCA carry-over; minimum health needed to clear this chart
  - must be in range 0-1 inclusive
- `#AUTHOR` str?
  - charter's name
- `#PREVIEW_TIME` float
  - time which the song preview starts
- `#PREVIEW_DURATION` float
- `#MOVIE <str?>` str?
  - **ORIGINAL TAG**
  - name of background video file to play
- `#MOVIEOFFSET` float?
  - **ORIGINAL TAG**
- `#BODY`
  - **ORIGINAL TAG**
  - marks the beginning of chart data

*`?` = tag is optional

> [!IMPORTANT]
> For compatibility reasons, the tags defined here are used **in addition to the original chart format's tags**.
