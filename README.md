# Amazon Phones Scraping Project

This project consists of scraping phone data from Amazon using Python, `aiohttp`, and `BeautifulSoup`. The project is divided into two main parts:
1. Scraping Amazon phone product links.
2. Scraping detailed information about the phones.

## Table of Contents
- [Project Overview](#project-overview)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Files](#files)
- [Dependencies](#dependencies)


## Project Overview

This project scrapes Amazon's phone product pages to gather product links and extract specific details about each phone model. The scraped data is saved in CSV files. 

### Steps involved:
1. **Scraping Links:** Extracts phone product URLs from Amazon's mobile section.
2. **Scraping Products:** Extracts detailed product information such as brand, color, OS, CPU, screen size, battery capacity, and user reviews.

## Features

- Asynchronous scraping using `aiohttp` to efficiently handle multiple page requests concurrently.
- Randomized User-Agent headers to minimize the risk of blocking.
- Retry mechanism for handling failed requests.
- Extracts key product details such as price, ratings, specifications, and user reviews.

## Installation

### Prerequisites

Before running the project, ensure that you have the following installed:
- Python 3.x
- `aiohttp`, `requests`, `BeautifulSoup`, `pandas`, `nest_asyncio`

To install the required libraries, run:

```bash
pip install aiohttp beautifulsoup4 pandas nest_asyncio requests
```

### Clone the Repository

```bash
git clone https://github.com/yourusername/amazon-phones-scraping.git
cd amazon-phones-scraping
```

## Usage

### 1. Scraping Links

Run the `amazon_phones_scraping.ipynb` notebook or Python script to start scraping product links:

```bash
python amazon_phones_scraping_links.py
```

This will:
- Gather phone product URLs.
- Save the URLs in `links.csv`.

### 2. Scraping Product Details

Run the following script to scrape the detailed phone information:

```bash
python amazon_phones_scraping_products.py
```

This will:
- Scrape detailed information such as product description, technical specifications, pricing, reviews, and more.
- Save the scraped data in `products.csv`.

## Files

- `amazon_phones_scraping_links.py`: Script to scrape Amazon phone product URLs.
- `amazon_phones_scraping_products.py`: Script to scrape detailed phone product information.
- `links.csv`: CSV file that contains the scraped product URLs.
- `products.csv`: CSV file with detailed product information.

## Dependencies

- `aiohttp`: For asynchronous HTTP requests.
- `BeautifulSoup4`: For parsing HTML.
- `pandas`: For managing data in DataFrames.
- `requests`: For synchronous HTTP requests (used in the product scraping stage).
- `nest_asyncio`: To allow nested asynchronous loops in notebooks.


