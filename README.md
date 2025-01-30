# Amazon Product Scraper

## Overview
This project is a web scraping application that extracts product details from Amazon using Python. The scraped data is saved in a CSV file for further analysis.

## Features
- Extracts product title, price, rating, bullet points, description, and reviews.
- Saves extracted data into a CSV file.
- Uses `BeautifulSoup` and `requests` for web scraping.

## Requirements
Ensure you have the following dependencies installed before running the script:

```sh
pip install beautifulsoup4 requests lxml
```

## Usage
1. Clone this repository or download the script.
2. Modify the `url` variable to point to the desired Amazon product page.
3. Run the script:
   
   ```sh
   python app.py
   ```
4. The extracted data will be saved in `amazon_airpod_pro_max.csv`.

## Code Explanation
- **Requests Module**: Fetches the HTML content of the Amazon product page.
- **BeautifulSoup**: Parses the HTML and extracts relevant product information.
- **CSV Module**: Saves the extracted data into a structured CSV file.

## Important Notes
- Amazon has strong anti-scraping mechanisms. If you receive a CAPTCHA page, consider:
  - Using a different User-Agent string.
  - Implementing request delays.
  - Using Selenium or a proxy service.
- The script may need adjustments if Amazon changes its HTML structure.

## Disclaimer
This project is intended for educational purposes only. Scraping Amazon without permission may violate their terms of service. Use responsibly.


