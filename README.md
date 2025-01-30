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

```py            
      url = "https://www.amazon.com/New-Apple-AirPods-Max-Blue/dp/B08PZJN7BD/ref=sr_1_1_sspa?crid=16VPECRWSHSU8&dib=eyJ2IjoiMSJ9.cAD_qAApnyUKwmxqHeslwy5KLVxWN5QeM4D9vx9PLtX9P9-f0xA5c0An0vT7aVmbI9ACVXckC06xo46oSSl0EHrya8enGiAlclNfEcxoKytG38imWJLQjhmMhBori20vm94LnkW5-QdMQIeQvS8DxLvYTtjhM7PksCMOozjfC-KhwaqvlcGU_YCjEzG6ovQXt62eZGx9zFk6-pl0ei4XtdieGKcW9Vc8uORYIZheTwY.9F3Lk9LaxnU6II-voUhHOzn2F8h1uHQeOitWaTO2Whg&dib_tag=se&keywords=apple%2Bairpods%2Bmax&qid=1738184134&sprefix=apple%2Bairpods%2Bmax%2Caps%2C173&sr=8-1-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&th=1"
      headers ={"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/132.0.0.0 Safari/537.36",
                "Accept-Language": "en-US,en;q=0.9",
                "Referer": "https://www.amazon.com/",
                "DNT": "1",
                "Upgrade-Insecure-Requests": "1",
                "Connection": "keep-alive"}
      
      response = requests.get(url,headers=headers)
      
      #print(response.text[:1000])  # Print the first 1000 characters of the HTML
      
      if response.status_code == 200 :
          print(response.status_code)
          html_content = response.text
      
      else:
          print("Fetching Error", response.status_code)
  ```    
  - **BeautifulSoup**: Parses the HTML and extracts relevant product information.
   ```py  
         soup = BeautifulSoup(html_content,'lxml')
         
         #print(soup.prettify())
         
         product_title = soup.find("span", id="productTitle").text.strip()
         product_price = soup.find("span", class_="a-price-whole").text.strip()
         product_rating = soup.find("span",id="acrPopover").text.strip()
         product_bp = soup.find("ul",class_="a-unordered-list a-vertical a-spacing-mini").text.strip()
         product_description = soup.find("div",class_="a-expander-content a-expander-section-content a-section-expander-inner").text.strip()
         product_review_USA = soup.find("ul",id="cm-cr-dp-review-list").text.strip()
         product_review_Globe = soup.find("ul",id="cm-cr-global-review-list").text.strip()
         
   ```        
- **CSV Module**: Saves the extracted data into a structured CSV file. 
  ```py
         with open("amazon_airpod_pro_max.csv",mode='w',newline='',encoding='utf-8') as file:
              writer =csv.writer(file)
              writer.writerow(["product_title","product_price","product_rating","product_bp","product_description","product_review_USA"])
              writer.writerow([product_title,product_price,product_rating,product_bp,product_description,product_review_USA])
  ```  
## Important Notes
- Amazon has strong anti-scraping mechanisms. If you receive a CAPTCHA page, consider:
  - Using a different User-Agent string.
  - Implementing request delays.
  - Using Selenium or a proxy service.
- The script may need adjustments if Amazon changes its HTML structure.

## Disclaimer
This project is intended for educational purposes only. Scraping Amazon without permission may violate their terms of service. Use responsibly.


