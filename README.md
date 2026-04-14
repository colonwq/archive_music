# archive_music — Dead & Company Internet Archive browser

A small, dependency-free web page that lists and filters live recordings from the [DeadAndCompany](https://archive.org/details/DeadAndCompany) collection on the Internet Archive. Everything runs in the browser; there is no backend.

## Contents

| File | Description |
|------|-------------|
| `dead-and-company-browser.html` | Single HTML file (markup, styles, and script). Open in a modern browser or serve locally. |

## Quick start

1. Open `dead-and-company-browser.html` in **Google Chrome** (or another current browser).
2. The page loads collection data from Archive.org automatically (paginated API requests).
3. Use the filters and sort options, then use **Export CSV** if you want a spreadsheet of the **currently visible** rows.

If opening the file via `file://` causes network or CORS issues in your environment, serve the project directory over HTTP and open the page from `http://localhost`, for example:

```bash
npx --yes serve .
```

## What the app shows

- **Show date** — Concert date from item metadata (`date`).
- **Title** — Links to the item on archive.org; the internal identifier is shown below the title.
- **Venue** / **Location** — From `venue` and `coverage` (city/region) when the Archive has them.
- **Artist** — From `creator` (typically “Dead & Company”).
- **Upload date** — From `publicdate` or `addeddate`.
- **Encoding** — A coarse label inferred from the search index’s `format` field and the item `identifier` (for example 16-bit vs 24-bit FLAC, MP3 VBR). It reflects how the item is described in the index, not a full per-file technical audit.

## Data source

The page calls Archive.org’s **Advanced Search** API:

- Query: `collection:DeadAndCompany`
- Fields requested include: `identifier`, `title`, `creator`, `date`, `venue`, `coverage`, `publicdate`, `addeddate`, `format`

The collection size and metadata can change over time as items are added or updated on the Archive.

## Limitations

- Requires network access to `https://archive.org`.
- Encoding labels are heuristics; for authoritative technical detail, open the item on the Archive and inspect files and descriptions.
- Some rows may have missing venue or location if upstream metadata is incomplete.

## License

The HTML/CSS/JS in this repository is provided as-is for personal use. Recordings on the Internet Archive remain subject to their respective licenses and Archive.org terms.
