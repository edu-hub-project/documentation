---
sidebar_position: 4
---

# Utility Functions

Some extra functions I used in case something goes wrong or needs to be double checked.

### Get a single meeting report

It saves a report from a single meeting, both in a human readable `.csv` and a `.json` that was uploaded in the old platform (unsure if this will still be relevant, but usually easier to manipulate via code).

It requires the `meeting_id` (the zoom one). At the moment it does not uses limesurvey.

### Get participants of more meetings

It reads all the meeting related to a single course (from zoom) and saves a single file with all meeting (each meeting is a row with date and the names of the participants).

It requires a `.csv` file with the following information:
```
title_course,
id_course,
link_zoom-meeting,
time-start
```
Actually, `id_course` is not yet used, so it can be skipped. Example: `VR Sessions Part II - 3,,23137084582,2020-12-18T16:55:37Z,2020-12-18T17:00:00Z
` (the zoom meeting was changed, it's most likely not valid).

It exists in two versions, one saving results in a human readable `.csv` and the other in a `.json` format.
