# Delhi accessibility viewer

An interactive map of how far people can travel by bus in Delhi, and how many jobs they
can reach, comparing today's timetable with one that runs twice as many buses.

**Open the site:** https://REPLACE-WITH-YOUR-GITHUB-PAGES-URL

## What you can do

| Control | What it does |
|---|---|
| **Map shows** | Travel time from one origin, jobs reachable from each hex, places reachable, or the jobs layer itself |
| **Network** | Baseline (today's buses), Revised (twice the buses), or the difference |
| **Departure** | The hour the trip starts, 00:00 to 23:00 |
| **Threshold** | The travel-time limit, 5 to 120 minutes |
| **Origin hex** | Click any hex, or paste a hex id |
| **Bus stops / Street map** | Extra layers |

Hover any hex for its id, the jobs in it, and its travel time in both networks.

## How to read it

- Every hexagon is about 450 m across (H3 resolution 9).
- Travel times are door to door: walking to the stop, waiting, riding, changing buses,
  and walking at the other end.
- Each trip starts exactly on the hour shown.
- "Jobs" are the jobs in the destination hexes, from the jobs layer.

## Accuracy

- **Travel time from an origin** is stored for one hex per 1.2 km cell. Clicking a hex
  uses the stored origin for its cell, at most about 600 m away. The map says so when
  that happens.
- Travel times are stored to the **nearest 2 minutes**, up to 180 minutes.
- **Jobs and places reachable** are exact for every hex and hour.

## What is in this repository

```
index.html        the viewer
lib/              maplibre-gl and h3-js (no internet needed for these)
data/meta.json    hexes, sample origins, bus stops, jobs per hex
data/*.bin.gz     jobs and places reachable per hex and hour; average trip parts
data/origins/     travel times from each stored origin, one file per origin
```

The street basemap comes from OpenStreetMap and needs internet; everything else is in
this repository.

## Where the numbers come from

Travel times were computed with ULTRA/RAPTOR over the Delhi bus GTFS and the OpenStreetMap
walking network, for every pair of 8,192 hexes and every departure hour. The revised
timetable is the same routes with each gap between buses split in two.
