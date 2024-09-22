# Amazon Product Scraper

This project is a web scraper designed to extract product information from Amazon. The scraper uses `requests` and `BeautifulSoup` to collect various product details, including images, descriptions, pricing information, and reviews. The data is processed, cleaned, and saved to a CSV file for further analysis.

## Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [How It Works](#how-it-works)
- [File Structure](#file-structure)
- [Data Processing](#data-processing)
- [Usage](#usage)
- [Output](#output)
- [Contributing](#contributing)
- [License](#license)

## Project Overview

This project scrapes product data from Amazon pages, including attributes such as price, ratings, descriptions, and customer reviews. After scraping, the data is cleaned and saved to a CSV file for further analysis.

## Features

- Extracts product details such as:
  - Name, brand, color, dimensions
  - Price, typical price, discounts
  - Number of ratings, reviews, and status
  - Buyer data (e.g., number of buyers last month)
- Extracts customer reviews (USA and international)
- Handles retries and failures in case of request timeouts
- Saves data to CSV for easy access and analysis

## Prerequisites

Before running the project, ensure you have Python 3.x installed on your machine along with the required libraries.

### Required Libraries

- `requests`
- `beautifulsoup4`
- `pandas`
- `concurrent.futures`

You can install the necessary Python packages by running:

```bash
pip install -r requirements.txt
```

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/your-username/amazon-product-scraper.git
   cd amazon-product-scraper
   ```

2. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Place the input CSV file (`links.csv`) with a column named `URL` containing product URLs in the root directory.

4. Run the script:

   ```bash
   python scraper.py
   ```

## How It Works

### Scraping Logic

- The scraper uses multiple user agents to avoid detection and blocks from the website.
- It makes HTTP requests using a retry mechanism to handle timeouts or server errors.
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
amazon-product-scraper/
│
├── scraper.py          # Main script to scrape and process data
├── requirements.txt    # Python dependencies
├── links.csv           # Input file containing URLs of Amazon products to scrape
└── amazon_product_data.csv  # Output CSV file containing scraped and cleaned data
```

- **`scraper.py`**: The main script responsible for scraping, processing, and saving the data.
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

To run the scraper:

1. Ensure that the `links.csv` file is properly set up with a column `URL` containing the product links.
2. Run the script with:

   ```bash
   python scraper.py
   ```

3. After scraping is complete, the output will be saved as `amazon_product_data.csv`.

### Example CSV (`links.csv`)

```csv
URL
https://www.amazon.com/dp/example-product-id-1
https://www.amazon.com/dp/example-product-id-2
```

### Example Usage in Jupyter/Colab

```python
import pandas as pd

# Load the scraped data
df = pd.read_csv('/content/amazon_product_data.csv')

# Display the first few rows
df.head()
```

## Output

The script generates a CSV file (`amazon_product_data.csv`) containing all the extracted and cleaned product details.

### Sample Output Columns

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

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

Feel free to modify the content as needed and replace any placeholder information like GitHub URLs and your own details. Let me know if you need further adjustments!
