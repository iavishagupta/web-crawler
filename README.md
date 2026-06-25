# Async Web Crawler

An asynchronous web crawler built with Python that recursively crawls a website, extracts useful page information, and generates a structured JSON report.

The crawler is capable of traversing internal pages concurrently while avoiding duplicate visits through URL normalization and thread-safe state management.

---

## Features

- Asynchronous crawling using `asyncio` and `aiohttp`
- Configurable concurrency limit
- Configurable maximum pages to crawl
- Internal-domain crawling only
- URL normalization to prevent duplicate crawling
- Thread-safe visited URL tracking
- HTML content extraction using BeautifulSoup
- Extracts:
  - Page heading
  - First paragraph
  - Outgoing links
  - Image URLs
- Generates structured JSON crawl report
- Unit tests included

---

## Project Structure

```
.
├── async_crawler.py        # Asynchronous crawler implementation
├── crawl.py                # Synchronous crawler implementation
├── client.py               # HTTP client
├── extract_html.py         # HTML parsing utilities
├── json_report.py          # JSON report writer
├── main.py                 # CLI entry point
├── report.json             # Generated crawl output
├── test_crawl.py           # URL normalization tests
├── test_extract_html.py    # HTML extraction tests
└── README.md
```

---

## Installation

Clone the repository

```bash
git clone <repository-url>
cd web-crawler
```

Install dependencies

```bash
pip install aiohttp beautifulsoup4 validators requests
```

---

## Usage

Basic crawl

```bash
python main.py https://example.com
```

Specify maximum concurrency

```bash
python main.py https://example.com 10
```

Specify both concurrency and page limit

```bash
python main.py https://example.com 10 100
```

Arguments

| Argument | Description |
|----------|-------------|
| URL | Website to crawl |
| Concurrency | Maximum simultaneous requests |
| Max Pages | Maximum number of pages to crawl |

---

## Example Output

```json
{
  "example.com/": {
    "url": "https://example.com/",
    "heading": "Home",
    "first_paragraph": "Welcome to our website.",
    "outgoing_links": [
      "https://example.com/about"
    ],
    "image_urls": [
      "https://example.com/logo.png"
    ]
  }
}
```

---

## How It Works

1. Validate the supplied URL.
2. Start crawling from the base page.
3. Download HTML asynchronously.
4. Parse page contents.
5. Store extracted information.
6. Discover internal links.
7. Skip already visited pages.
8. Continue until the maximum page limit is reached.
9. Export results to `report.json`.

---

## Technologies Used

- Python 3
- asyncio
- aiohttp
- BeautifulSoup4
- requests
- urllib.parse
- unittest

---

## Current Architecture

```
           Base URL
               │
               ▼
      Async Web Crawler
               │
      ┌────────┴────────┐
      ▼                 ▼
 Download HTML     Track Visited URLs
      │
      ▼
 Parse HTML
      │
      ▼
 Extract Data
      │
      ▼
 Discover Links
      │
      ▼
 Schedule New Crawl Tasks
      │
      ▼
 Generate JSON Report
```

---

## Future Improvements

- Queue-based worker architecture
- robots.txt compliance
- Retry with exponential backoff
- Request timeouts
- Persistent crawl database
- URL canonicalization improvements
- Crawl statistics dashboard
- Sitemap generation
- Logging framework
- Support for incremental crawling

---

## Running Tests

Run all tests

```bash
python -m unittest
```

Or individually

```bash
python test_crawl.py
python test_extract_html.py
```

---

## Learning Objectives

This project demonstrates practical implementation of:

- Asynchronous programming
- Concurrent task scheduling
- Web crawling
- HTML parsing
- URL normalization
- Thread-safe shared state
- Python testing
- Clean project organization

---

## License

This project is intended for educational and portfolio purposes.
