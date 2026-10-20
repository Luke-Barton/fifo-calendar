# fifo-calendar

My FIFO roster calendar. One HTML file (`fifo_calendar.html`) hosted on GitHub Pages and shown on my phone home screen with WebsiteWidget.

## Crews

- **A/B crew** (code `AB`) — was called "Crew B" in older versions
- **C/D crew** (code `CD`) — was called "Crew A" in older versions

Same 14-day cycle, offset by 7 days. A swing is 8 days (travel in Tue, work Wed to Mon, travel out Tue), then 6 days off.

## Updating it

On GitHub: open `fifo_calendar.html` → pencil icon → edit → **Commit changes**. Live in a minute or two.

All edits go in the `<script>` section near the middle of the file. Dates are always `"YYYY-MM-DD"` in quotes.

| I want to… | Edit this | Section |
|---|---|---|
| Add planned leave / a holiday | `LEAVE` | 1D |
| Fly home early, add an extra day, swap a day | `ROSTER_CHANGES` | 1C |
| Change which crew I'm on | `CREW_PERIODS` | 1B |
| Add public holidays, birthdays, sport events | `PUBLIC_HOLIDAYS`, `BIRTHDAYS`, `SPORTS` | 2–4 |

### Add leave

```js
const LEAVE = [
  { from: "2026-12-24", to: "2027-01-04", label: "Xmas hols" },  // a range
  { from: "2027-03-12", label: "Wedding" },                      // a single day
];
```

Leave shows teal and replaces work / travel / off on those days. Labels fit about 10 characters.

### One-off roster changes

```js
const ROSTER_CHANGES = [
  { from: "2026-11-20", status: "travel" },                          // flying home
  { from: "2026-11-21", to: "2026-11-23", status: "off" },           // home early
];
```

`status` is `"travel"`, `"work"` or `"off"`.

### Switch crew

```js
const CREW_PERIODS = [
  { from: "2026-10-07", crew: "AB" },
  { from: "2026-10-27", crew: "CD" },
  // { from: "2027-02-02", crew: "AB" },   // example: switch back
];
```

Keep entries in date order. Days before the first entry are blank.

## Priority

For any day: **LEAVE > ROSTER_CHANGES > normal crew pattern.** The countdown banner and "Day N" numbers are worked out from what's actually on the calendar, so early flights and leave are counted correctly.
