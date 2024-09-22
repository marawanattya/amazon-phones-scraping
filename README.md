# Amazon Product Scraper

## Project Overview

This project is an **asynchronous web scraper** designed to extract product information from Amazon product listings. It uses `aiohttp` for making concurrent HTTP requests and `BeautifulSoup` for parsing HTML to extract data. The scraper also includes additional logic for data extraction, error handling, and retries.

The project has two parts:
1. **Async Scraper (using `aiohttp`)**: Fetches URLs and collects product listing links asynchronously.
2. **Synchronous Scraper (using `requests`)**: Extracts product details like title, price, ratings, and reviews from the collected URLs.

## Features

- Uses asynchronous programming to scrape URLs concurrently, significantly speeding up the scraping process.
- Extracts detailed product information such as:
  - Product title
  - Price
  - Ratings and number of reviews
  - Product specifications like color, OS, CPU, etc.
  - Reviews (if available)
- Includes random user-agent headers and timeouts to avoid getting blocked.
- Resilient to errors with retry mechanisms.

## Project Structure

```
├── async_scraper.py   # Asynchronous web scraping script
├── sync_scraper.py    # Synchronous web scraping and data extraction
├── README.md          # This file
├── links.csv          # File containing the scraped product URLs
└── requirements.txt   # Dependencies for the project
```

## Setup and Installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/yourusername/amazon-product-scraper.git
   cd amazon-product-scraper
   ```

2. **Install dependencies:**

   Make sure you have Python 3.8+ installed. Then install the required libraries:

   ```bash
   pip install -r requirements.txt
   ```

3. **Create a CSV file with product URLs:**

   The `async_scraper.py` script will generate `links.csv` file that contains product URLs. You can customize the URL patterns in the script to fit your requirements.

## Usage

### 1. Asynchronous URL Scraping

The `async_scraper.py` script gathers Amazon product URLs and saves them in `links.csv`.

**Running the asynchronous scraper:**

```bash
python async_scraper.py
```

This script:
- Scrapes Amazon product listings and collects product URLs asynchronously.
- Stores the collected URLs in a CSV file (`links.csv`).

### 2. Synchronous Product Data Scraping

Once URLs are collected, the `sync_scraper.py` script extracts detailed product information.

**Running the synchronous scraper:**

```bash
python sync_scraper.py
```

This script:
- Reads URLs from `links.csv`.
- Scrapes individual product pages.
- Extracts relevant data like product details, ratings, and reviews.
- Saves the data to a structured format (e.g., JSON, CSV, etc.).

## Key Functions

### `async_scraper.py`
- **`get_html()`**: Asynchronously fetches HTML from a given URL.
- **`extract_job_links()`**: Extracts product links from the search page.
- **`scrape_page()`**: Scrapes multiple pages concurrently using `asyncio`.
- **`main()`**: Orchestrates the scraping, gathering product URLs.

### `sync_scraper.py`
- **`scrap_page()`**: Extracts detailed product information (price, ratings, etc.).
- **`scrap()`**: Fetches and parses the HTML for individual product pages.
- **`get_html()`**: Fetches HTML from a given URL using a random user-agent to simulate human behavior.

## Logging and Error Handling

- The scrapers use logging to track the progress and errors. Any failed requests are retried multiple times.
- A random delay is added between requests to avoid being blocked by Amazon.

## Future Enhancements

- Adding support for scraping more categories and filters.
- Adding a feature for saving data to different formats (JSON, Excel).
- Implementing rate-limiting logic for avoiding blocks more effectively.

## License

This project is licensed under the MIT License. See the `LICENSE` file for more details.
