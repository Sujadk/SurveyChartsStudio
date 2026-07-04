# SurveyChartsStudio

SurveyChartsStudio is a client-side, single-page web app for turning survey responses into high-contrast charts that stay readable in print, photocopies, and grayscale exports. It runs entirely in the browser, so there is no backend, database, or account setup required.


 live url link: https://surveychartsstudio.netlify.app/
## What It Does

The app focuses on a few practical survey workflows:

- Upload CSV, TSV, JSON, Excel, PDF, or image files and extract survey data in-browser.
- Detect whether the source is raw respondent data or already summarized counts.
- Render charts with monochrome-friendly patterns, leader lines, and bar labels.
- Export one chart or the whole dashboard as PNG files.
- Edit question text, response values, visibility, and chart type directly in the sidebar.

## Core Features

### Multi-Format Input Parsing

The application detects file types from extension or content sniffing and implements custom client-side parsing routines for:

- Tabular data formats: CSV, TSV, JSON, and Excel (`.xlsx`, `.xls`) files.
- Google Forms summary exports: Text-based PDFs and raw copy-pasted text.
- Charts and tables: Extraction of labels and numerical values from images (PNG, JPG) using client-side Optical Character Recognition (OCR) fallback.

### Accessible Grayscale Rendering

To ensure readability when printed or photocopied in pure black-and-white, the application implements:

- **Monochrome Patterns**: Dynamic generation of eight distinct high-contrast canvas pattern fills (solid, diagonal lines, back-diagonal lines, cross-hatch, dots, dense diagonal lines, horizontal lines, and vertical lines) overlaid on colors.
- **Non-Overlapping Radial Leader Lines**: A custom Chart.js plugin that projects slice boundaries radially outward to staggered text labels, utilizing a Y-coordinate relaxation algorithm to prevent text collisions.
- **Direct Bar Annotations**: Exact values and percentages displayed adjacent to horizontal or vertical bars to negate dependencies on scale colors.

### High-DPI Exports

- Export individual charts as PNGs named following the `{question_slug}_{chart_type}.png` convention.
- Export the entire dashboard as a stacked-grid PNG layout at 2x pixel density.
- On-screen print verification via a grayscale simulation toggle.

## How The Data Flow Works

1. Files and pasted text are routed through the parser that best matches the input type.
2. Parsed questions are stored in the in-memory survey state.
3. The editor lets you clean up labels and counts before rendering.
4. Chart.js draws the final visualizations with patterns and accessibility-friendly annotations.

## Supported Inputs

- Tabular files: CSV, TSV, XLSX, XLS, and JSON.
- Google Forms-style summary text copied from a report or PDF.
- Image uploads and clipboard images through OCR fallback.

## Output Notes

- Pie and donut charts use radial labels to avoid overlap.
- Bar charts can show either counts, percentages, or both.
- The dashboard export is intended for reports, handouts, and print-ready review.

## Technical Architecture

The application is built using a serverless, client-side architecture requiring no backend database or network dependencies.

- **Rendering Framework**: Chart.js (v4.4.1) UMD
- **CSV Parsing**: PapaParse (v5.4.1)
- **Spreadsheet Parsing**: SheetJS (v0.18.5)
- **PDF Scraping**: PDF.js (v3.11.174)
- **In-Browser OCR**: Tesseract.js (v5.0.0)
- **DPI Scaling**: html2canvas (v1.4.1)

## Setup and Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/Sujadk/SurveyChartsStudio.git
   ```
2. Open `index.html` in any modern web browser.
3. Drop in a survey file, paste summary text, or use one of the sample buttons to see the parser in action.
4. No build steps, installations, or local server instances are required for basic usage.

## Repository Notes

- The main application logic lives in `index.html`.
- The app name in the page metadata now matches the README spelling, `SurveyChartsStudio`.
- Function names were clarified to better reflect their role in the upload, parsing, editor, and export flow.

## License

This project is licensed under the Apache License 2.0. Refer to the LICENSE file for details.
