# Web Scraping with Python Selenium: Tutorial for Beginners

[![Oxylabs promo code](https://user-images.githubusercontent.com/129506779/250792357-8289e25e-9c36-4dc0-a5e2-2706db797bb5.png)](https://oxylabs.go2cloud.org/aff_c?offer_id=7&aff_id=877&url_id=112)


[<img src="https://img.shields.io/static/v1?label=&message=python&color=brightgreen" />](https://github.com/topics/python) [<img src="https://img.shields.io/static/v1?label=&message=selenium&color=blue" />](https://github.com/topics/selenium) [<img src="https://img.shields.io/static/v1?label=&message=Web%20Scraping&color=important" />](https://github.com/topics/web-scraping)
- [Installing Selenium](#installing-selenium)
- [Testing](#testing)
- [Scraping with Selenium](#scraping-with-selenium)

In this article, we’ll cover an overview of web scraping with Selenium using a real-life example.

For a detailed tutorial on Selenium, see [our blog](https://oxylabs.io/blog/selenium-web-scraping).

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

For a detailed tutorial on Selenium, see [our blog](https://oxylabs.io/blog/selenium-web-scraping).
