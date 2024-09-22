# Amazon Phones Scraping Project

This project scrapes Amazon for product links and detailed information about mobile phones, using Python for asynchronous web scraping. The goal is to collect and store details such as prices, ratings, product descriptions, and other specifications of mobile phones listed on Amazon.

## Project Overview

The project is split into two stages:

1. **Scraping Product Links**: Using asynchronous scraping with `aiohttp`, we collect links to individual mobile phone product pages from Amazon.
2. **Scraping Product Details**: Once the product links are gathered, another script scrapes detailed information about each mobile phone, including its features, specifications, and customer reviews.

## Features

- Asynchronous scraping of multiple pages using `aiohttp` and `asyncio`.
- Collection of mobile phone product links across multiple pages of Amazon search results.
- Extracts product details such as:
  - Name, brand, color, dimensions
  - Price, typical price, discounts
  - Number of ratings, reviews, and status
  - Buyer data (e.g., number of buyers last month)
- Extracts customer reviews (USA and international)
- Handles retries and failures in case of request timeouts
- Saves data to CSV for easy access and analysis

## Prerequisites

Before running the scripts, ensure you have the following installed:

- Python 3.x
- Libraries:
  - `aiohttp`
  - `nest_asyncio`
  - `beautifulsoup4`
  - `pandas`
  - `requests`
  - `concurrent.futures`
  - `lxml`

Install these dependencies using:

```bash
pip install aiohttp nest_asyncio beautifulsoup4 pandas requests lxml
```

## How It Works

### Scraping Logic

1. **Scraping Product Links** (`amazon_phones_scraping.ipynb`): 
    - The script starts by scraping mobile phone listings on Amazon.
    - For each page, it collects the product links using the `aiohttp` library and stores them in a set to ensure uniqueness.

2. **Scraping Product Details** (`amazon_phones_scraping_products.ipynb`):
    - After collecting product URLs, a second script is used to extract detailed product information from each page.
    - It uses the `requests` library with randomized user agents and retries to avoid rate-limiting or blocking.
    - Extracted product details include:
      - **Basic Info**: name, brand, color, model, etc.
      - **Pricing Info**: price, typical price, discounts, savings
      - **Ratings & Reviews**: number of ratings, reviews (USA and international)
      - **Specifications**: battery capacity, storage, screen size, CPU, etc.



### Data Cleaning and Processing

Once data is collected from the HTML page, it is cleaned and processed. This includes:
- Converting string prices and numbers (with symbols like `$`, `,`, and `K`) to numeric values.
- Calculating the `you_save` column by subtracting the product's current price from the typical price.

The processed data is saved as a CSV file (`amazon_product_data.csv`), which can be easily loaded into a DataFrame for further analysis.


## File Structure

```
├── amazon_phones_scraping.ipynb          # The main script responsible for scraping, processing, and saving the data.
├── links.csv                             # Output file containing scraped product URLs
├── amazon_product_data.csv               # Output CSV file containing scraped and cleaned data
└── README.md                             # Project documentation (this file)
```

- **`amazon_phones_scraping.ipynb`**: The main script responsible for scraping, processing, and saving the data.
- **`links.csv`**: A CSV file with a list of Amazon product URLs to scrape.
- **`amazon_product_data.csv`**: Output file that stores the scraped product data.


## Data Processing

The following columns are processed and cleaned in the output CSV:

- **typical_price**: Typical price of the product, stripped of `$` and `,`, converted to float.
- **number_of_buyers_last_month_more_than**: Number of buyers last month, replacing 'K' with '000' and removing `+`.
- **number_of_ratings**: Number of product ratings, stripped of commas.
- **price**: Current price, stripped of `$` and `,`, converted to float.
- **you_save**: Calculated field showing the amount saved (`typical_price - price`).

The processed DataFrame is saved to `amazon_product_data.csv`.

  
## Usage

1. **Step 1**: Run the `amazon_phones_scraping.ipynb` section scrap links to scrape product links.
   - This will scrape multiple pages on Amazon and save all product links to `links.csv`.

2. **Step 2**: Run the `amazon_phones_scraping.ipynb` section scrap products to scrape product details.
   - This script reads `links.csv`, visits each link, scrapes the product details, and saves them to `amazon_product_data.csv`.

## Output

The script generates a CSV files
- **links.csv**: A CSV file containing all scraped product URLs.
- **amazon_product_data.csv**: containing all the extracted and cleaned product details.

### Sample Output Columns
- **URL**: Product URL
- **name**: Product name
- **brand**: Product brand
- **price**: Current price
- **typical_price**: Previous/typical price
- **you_save**: Difference between typical price and current price
- **number_of_ratings**: Total ratings
- **reviews_usa**: Top 5 USA reviews
- **reviews_other**: Top 5 international reviews
- **discount**: Discount percentage (if available)
- **color**: Product color

## Contributing

Contributions are welcome! If you encounter any issues or have ideas for improvements, feel free to open a pull request or issue on GitHub.


