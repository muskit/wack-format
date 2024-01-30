# 🏗 UNDER CONSTRUCTION
This format is still being developed.
- Details like package topology and .mer tags are not final!!
- Check commit history to see changes

# wack Format
This document details the specifications of the "wack" package for containing a song's *audio*, *metadata*, and *charting* information.

# Table of Contents
1. [Topology](#topology)
    - [Song Folder Contents](#song-folder-contents)
    - [.wack Package File](#wack-package-file)
2. [mer Files](#mer-files)
    - [metadata .mer](#metadata-mer)
    - [Chart .mer](#chart-mer)

# Topology
**A song is packaged as a folder**. Songs can be nested in subfolders for organization purposes. However, a single file -- `meta.mer` -- must be present to define its folder as a song (detailed later).

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
**TODO**: .hca audio

## .wack Package File
**A directory structure of song folders may placed into a zip file with the extension `.wack` for transferring purposes.** Applications implementing this format may accept .wack files, but it is advisable to store the song folders contained (with structure preserved) in the long-term.

# .mer Files
There are two types of .mer files in a song: *metadata* and *charts*. Both types are detailed in the following subsections.

> [!WARNING]
> For any .mer file, **tags not defined in this document may be added**. Tags may also be stored out of order. Please keep this in mind when consuming.

## Metadata .mer
**This file, named `meta.mer`, must be present to define its folder as a song.**

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
  - a carry-over from WACCA
  - can be used for sub-text not related to copyright
  - **TODO**: rename to `#SUBTEXT`? deliberation needed
- `#GENRE` str?
  - a carry-over from WACCA
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
