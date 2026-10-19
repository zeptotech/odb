# ODB Formulary Search

A fast, print-friendly search tool for the Ontario Drug Benefit (ODB) formulary, designed for prescribers and pharmacists. Runs entirely as a static site on GitHub Pages — no backend required.

**Live site: https://zeptotech.github.io/odb/**

## Current data

**Formulary XML date:** 2026-09-22

The formulary date is also shown in the site header and on every printout.

## Features

- Search by generic name (ingredient), brand name, or DIN
- Shows ODB coverage status: General Benefit, Limited Use, or Not a Benefit
- Displays Limited Use codes and authorization periods at a glance
- Click any result to expand the full LU criteria in a clear two-column layout
- Print-optimized portrait layout with prominent LU codes

## Using the site

Go to **[zeptotech.github.io/odb](https://zeptotech.github.io/odb/)**. Type any part of a drug name, brand name, or an 8-digit DIN into the search box.

## Updating the formulary data

The Ontario government publishes an updated formulary XML file every few months at:
**[formulary.health.gov.on.ca](https://www.formulary.health.gov.on.ca/formulary/)**

When a new XML is released:

1. Download the new XML file and replace `formulary.xml` in this repo
2. Run the build script to regenerate the JSON:
   ```
   python3 build.py
   ```
   The build copies the XML's `createDate` into `formulary.json` as `generated`, which the site displays as the formulary date. To check the date of a downloaded XML:
   ```
   head -c 200 formulary.xml
   ```
3. Update the formulary XML date under **Current data** at the top of this README
4. Commit and push:
   ```
   git add formulary.xml formulary.json README.md
   git commit -m "Update formulary data to YYYY-MM-DD"
   git push
   ```

GitHub Pages will redeploy automatically within a minute or two.

## Files

| File | Purpose |
|---|---|
| `formulary.xml` | Source data from Ontario government (do not edit manually) |
| `build.py` | Converts `formulary.xml` → `formulary.json` |
| `formulary.json` | Processed data served to the browser (generated — do not edit manually) |
| `index.html` | Main page |
| `style.css` | Styles including print layout |
| `app.js` | Search and rendering logic |

## GitHub Pages setup

In the repo settings, go to **Pages** → set source to **Deploy from a branch** → select **main** branch, **/ (root)** folder.
