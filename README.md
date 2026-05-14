# EVforall Incentives Scraper

A Node.js + Playwright scraper that collects **Charging Station Incentives** from the Electric For All rebates and incentives page for a list of ZIP codes.

The script visits the Electric For All incentives page, enters each ZIP code, waits for the charging station incentive cards to load, extracts the incentive text, and saves the results to a local `results.json` file.

## What This Tool Does

This scraper:

- Uses Playwright to launch a headless Chromium browser
- Visits `https://www.electricforall.org/rebates-incentives/`
- Searches incentives by ZIP code
- Extracts text from the **Charging Station Incentives** section
- Saves results incrementally to `results.json`
- Skips ZIP codes that have already been completed if `results.json` exists

## Project Files

- `scrape.js` — main scraper script
- `package.json` — project metadata and dependencies
- `package-lock.json` — exact locked dependency versions
- `.gitignore` — files/folders Git should ignore
- `README.md` — project documentation
- `results.json` — generated output file, usually not committed

## Requirements

Before running this project, make sure you have:

- Node.js 18 or newer
- npm

## Installation

Clone the repository:

```bash
git clone <your-repo-url>
cd <your-repo-folder>
```

Install dependencies:

```bash
npm install
```

Install Playwright browser binaries:

```bash
npx playwright install
```

## Usage

Run the scraper:

```bash
node scrape.js
```

The script will begin scraping incentives for each ZIP code.

Example terminal output:

```text
Scraping ZIP 35004
  Loading incentives for 35004...
  Saved 35004
Scraping ZIP 35005
  Loading incentives for 35005...
  Saved 35005
```

## Output

The scraper creates a file named:

```text
results.json
```

Example structure:

```json
{
  "35004": "Charging Station Incentives ...",
  "35005": "Charging Station Incentives ..."
}
```

Each key is a ZIP code, and each value is the scraped incentive text for that ZIP code.

## Resume Behavior

If the scraper stops or fails partway through, run it again:

```bash
node scrape.js
```

The script checks `results.json` and skips ZIP codes that were already completed.

This makes it safer to run the scraper over a long ZIP code list without starting over from the beginning.

## Recommended `.gitignore`

Create a file named `.gitignore` and add:

```gitignore
node_modules/
results.json
.DS_Store
```

Do not commit `node_modules/`. Other users can recreate it with:

```bash
npm install
```

You usually should not commit `results.json` unless you intentionally want to publish the scraped data.

## Notes

- The scraper runs Chromium in headless mode.
- Each ZIP code is processed one at a time.
- The script waits for the incentive cards to stabilize before extracting text.
- Failed ZIP codes are logged in the terminal but do not stop the entire scraper.

## Troubleshooting

### Playwright is not found

Run:

```bash
npm install
```

### Browser executable is missing

Run:

```bash
npx playwright install
```

### The scraper times out

The website may be loading slowly or may have changed its page structure. Try running the script again. If timeouts continue, the selectors or wait logic in `scrape.js` may need to be updated.

## License

ISC
