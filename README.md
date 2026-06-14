# GitHub Widget

An [Appinapp](https://appinapp.mutawirr.uz) desktop widget that renders your GitHub contribution graph for the current year, right on your macOS desktop.

![screenshot](https://github.com/developerbola/github.widget/blob/main/screenshot.png)

## Features

- Renders the current year's contribution calendar as a GitHub-style heatmap grid (7 rows, one column per week).
- Color intensity scales with daily commit count (`0`, `<5`, `<10`, `<20`, `20+`).
- Hover a cell to scale it up and reveal the commit count.
- Skeleton loading state while data is fetched.
- Auto-refreshes every hour.
- Sizes the grid to fit the configured window width.

## Requirements

- macOS with [Appinapp](https://appinapp.mutawirr.uz) installed.
- A GitHub [personal access token](https://github.com/settings/tokens) with read access to your contribution data (the GraphQL contributions API requires authentication).

## Installation

1. Locate your Appinapp widgets folder (default: `~/.appinapp`).
2. Copy this folder (`github.widget`) into it.
3. Open `index.jsx` and set your config (see below).
4. Übersicht reloads automatically; the widget appears on your desktop.

## Configuration

Edit the top of [index.jsx](index.jsx):

```js
const githubUsername = "developerbola"; // your GitHub username
const githubToken = "";                 // your GitHub personal access token
```

Optional window/layout settings (also in `index.jsx`):

| Constant            | Default   | Purpose                          |
| ------------------- | --------- | -------------------------------- |
| `windowWidth`       | `399`     | Widget width in px               |
| `windowHeight`      | `125`     | Widget height in px              |
| `windowLeft`        | `10`      | X position from screen left      |
| `windowTop`         | `35`      | Y position from screen top       |
| `refreshFrequency`  | `3600000` | Refresh interval in ms (1 hour)  |

> **Note:** The token is stored in plain text in `index.jsx`. Keep this file private and do not commit a real token.

## How it works

The widget queries the GitHub GraphQL API (`contributionsCollection.contributionCalendar`) for your contribution weeks, slices them down to the current calendar year, normalizes each week to 7 days, and renders a `<div>` grid. Out-of-year days are padded as empty cells so the grid stays rectangular.

## License

MIT
