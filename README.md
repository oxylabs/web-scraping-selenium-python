# Web Scraping with Python Selenium: Tutorial for Beginners

[![Oxylabs promo code](https://raw.githubusercontent.com/oxylabs/product-integrations/refs/heads/master/Affiliate-Universal-1090x275.png)](https://oxylabs.io/pages/gitoxy?utm_source=github&utm_medium=referral&utm_content=web-scraping-selenium-python&utm_campaign=banner&groupid=877)

<p align="left">
  <a href="https://dashboard.oxylabs.io"><img src="https://img.shields.io/badge/%F0%9F%9A%80_Get_Started-FF6B35?style=for-the-badge" alt="Get started"></a>
  <a href="https://developers.oxylabs.io/products/web-api"><img src="https://img.shields.io/badge/%F0%9F%93%9A_Documentation-4A90E2?style=for-the-badge" alt="Documentation"></a>
  <a href="https://dashboard.oxylabs.io"><img src="https://img.shields.io/badge/%F0%9F%93%8A_Dashboard-2EA44F?style=for-the-badge" alt="Dashboard"></a>
  <a href="https://discord.gg/Pds3gBmKMH"><img src="https://img.shields.io/badge/%F0%9F%92%AC_Discord-5865F2?style=for-the-badge" alt="Discord"></a>
  <a href="https://www.youtube.com/@oxylabs"><img src="https://img.shields.io/badge/%E2%96%B6%EF%B8%8F_YouTube-FF0000?style=for-the-badge" alt="YouTube"></a>
</p>

[<img src="https://img.shields.io/static/v1?label=&message=python&color=brightgreen" />](https://github.com/topics/python) [<img src="https://img.shields.io/static/v1?label=&message=selenium&color=blue" />](https://github.com/topics/selenium) [<img src="https://img.shields.io/static/v1?label=&message=Web%20Scraping&color=important" />](https://github.com/topics/web-scraping)

- [Installing Selenium](#installing-selenium)
- [Testing](#testing)
- [Scraping with Selenium](#scraping-with-selenium)

In this article, we’ll cover an overview of web scraping with Selenium using a real-life example.

For a detailed tutorial on Selenium, see [our blog](https://oxylabs.io/blog/selenium-web-scraping?utm_source=github&utm_medium=referral&utm_content=web-scraping-selenium-python&groupid=877).

## Installing Selenium

1. Create a virtual environment:

```sh
python3 -m venv .env
```

2. Install Selenium using pip:

```sh
pip install selenium
```

3. Install Selenium Web Driver. See [this page](https://www.selenium.dev/documentation/webdriver/getting_started/install_drivers/) for details.

## Testing

With virtual environment activated, enter IDLE by typing in `python3`. Enter the following command on IDLE:

```python
>>> from selenium.webdriver import Chrome

```

If there are no errors, move on to the next step. If there is an error, ensure that `chromedriver` is added to the PATH.

## Scraping with Selenium

Import required modules as follows:

```python
from selenium.webdriver import Chrome, ChromeOptions
from selenium.webdriver.common.by import By
```

Add the skeleton of the script as follows:

```python
def get_data(url) -> list:
   ...


def main():
    ...

if __name__ == '__main__':
    main()
```

Create ChromeOptions object and set `headless` to `True`. Use this to create an instance of `Chrome`.

```python
    browser_options = ChromeOptions()
    browser_options.headless = True

    driver = Chrome(options=browser_options)
```

Call the `driver.get` method to load a URL. After that, locate the link for the Humor section by link text and click it:

```python
    driver.get(url)

    element = driver.find_element(By.LINK_TEXT, "Humor")
    element.click()
```

Create a CSS selector to find all books from this page. After that run a loop on the books and find the bookt title, price, stock availability. Use a dictionary to store one book information and add all these dictionaries to a list. See the code below:

```python
 books = driver.find_elements(By.CSS_SELECTOR, ".product_pod")
    data = []
    for book in books:
        title = book.find_element(By.CSS_SELECTOR, "h3 > a")
        price = book.find_element(By.CSS_SELECTOR, ".price_color")
        stock = book.find_element(By.CSS_SELECTOR, ".instock.availability")
        book_item = {
            'title': title.get_attribute("title"),
            'price': price.text,
            'stock': stock. text
        }
        data.append(book_item)

```

Lastly, return the `data` dictionary from this function.

For the complete code, see [main.py](src/main.py).

For a detailed tutorial on Selenium, see [our blog](https://oxylabs.io/blog/selenium-web-scraping?utm_source=github&utm_medium=referral&utm_content=web-scraping-selenium-python&groupid=877).
