# Web Scraping Example with lxml

This example demonstrates how to scrape article titles and bio fields from a web page using Python's `requests` and `lxml` libraries.

## Prerequisites

* Python 3.x
* `requests` library
* `lxml` library

Install dependencies:

```bash
pip install requests lxml
```

## Usage

Save the code below to `scrape_example.py` and update the `url` variable. Then run:

```bash
python scrape_example.py
```

## Code Example

```python
import requests
from lxml import html

def scrape_page(url):
    # 1. Download the page
    response = requests.get(url)
    response.raise_for_status()  # Stop if there was an error

    # 2. Turn the raw HTML into something we can query
    doc = html.fromstring(response.content)

    # 3. Grab article titles (if you still need them)
    raw_titles = doc.xpath('//h2[@class="post-title"]/a/text()')
    titles = [t.strip() for t in raw_titles]  # clean up whitespace

    # 4. Find every bio field inside the 3-column block
    bio = {}
    #    This finds each <div class="c-bio__field"> inside the parent
    field_blocks = doc.xpath('//div[@class="c-bio__row--3col"]/div[@class="c-bio__field"]')

    for block in field_blocks:
        # 4a. In each block, get the label (e.g. "Octagon Debut")
        label_list = block.xpath('./div[@class="c-bio__label"]/text()')
        # 4b. …and the corresponding text (e.g. "Apr. 20, 2019")
        text_list  = block.xpath('./div[@class="c-bio__text"]/text()')

        if not label_list or not text_list:
            # skip if something’s missing
            continue

        # 4c. Clean and store them
        label = label_list[0].strip().rstrip(':')  # remove extra spaces/colons
        text  = text_list[0].strip()
        bio[label] = text

    # 5. Return everything in one simple dict
    return {
        'titles': titles,  # list of page titles
        'bio':    bio      # dict of bio fields
    }


if __name__ == "__main__":
    url = "https://example.com/page-with-bio"
    result = scrape_page(url)

    # Print the results nicely
    print("Article titles:")
    for i, title in enumerate(result['titles'], 1):
        print(f" {i}. {title}")

    print("\nBio details:")
    for name, value in result['bio'].items():
        print(f" • {name}: {value}")
```

```text

OUTPUT:

Article titles:
 1. First Blog Post
 2. Another Article
 3. Yet One More

Bio details:
 • Octagon Debut: Apr. 20, 2019
 • Reach: 72.50
 • Leg reach: 39.50

```
