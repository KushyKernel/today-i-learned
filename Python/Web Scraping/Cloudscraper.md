# Web Scraping with Cloudscraper

This example shows how to use the **cloudscraper** library to handle sites protected by Cloudflare. It’s perfect for more advanced scraping where standard `requests` may be blocked.

## Prerequisites

* Python 3.6 or newer
* `cloudscraper` library

Install with pip:

```bash
pip install cloudscraper
```

## Basic Usage

Save the code below to `scrape_cloudscraper.py` and update the `url`. Then run:

```bash
python scrape_cloudscraper.py
```

```python
import cloudscraper
from lxml import html

def scrape_with_cloudscraper(url):
    # 1. Create a scraper that can bypass Cloudflare
    scraper = cloudscraper.create_scraper()

    # 2. Fetch the page
    response = scraper.get(url)
    response.raise_for_status()

    # 3. Parse HTML for querying
    doc = html.fromstring(response.text)

    # 4. Example: extract all article titles
    titles = [t.strip() for t in doc.xpath('//h2[@class="post-title"]/a/text()')]

    # 5. Example: extract bio fields in 3-col block
    bio = {}
    fields = doc.xpath(
        '//div[@class="c-bio__row--3col"]/div[@class="c-bio__field"]'
    )
    for fld in fields:
        label = fld.xpath('./div[@class="c-bio__label"]/text()')
        text  = fld.xpath('./div[@class="c-bio__text"]/text()')
        if label and text:
            key = label[0].strip().rstrip(':')
            bio[key] = text[0].strip()

    return {
        'titles': titles,
        'bio': bio
    }

if __name__ == '__main__':
    url = 'https://example.com/protected-page'
    data = scrape_with_cloudscraper(url)

    print('Article titles:')
    for i, title in enumerate(data['titles'], 1):
        print(f' {i}. {title}')

    print('\nBio details:')
    for name, val in data['bio'].items():
        print(f' • {name}: {val}')
```

## Notes

* **Cloudscraper** automatically handles common anti-bot measures (JavaScript challenges, CAPTCHAs) without manual configuration.
* Use responsibly and respect the target site’s `robots.txt` and terms of service.
* For complex scenarios, you can pass custom headers or cookies to `create_scraper()`.

---

