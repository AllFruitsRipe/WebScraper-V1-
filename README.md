# Sample Code to be edited

import scrapy
from scrapy.crawler import CrawlerProcess


class Spidey(scrapy.Spider):
    name = "Spidey"

    def start_requests(self):
        url = 'INSERT_URL_HERE'  # Replace INSERT_URL_HERE with the actual URL
        yield scrapy.Request(url=url, callback=self.parse_one)

    def parse_one(self, response):
        # Extracting data from the webpage
        quote_header = response.xpath('XPATH_NOTATION_HERE').getall()  # Replace XPATH_NOTATION_HERE with the actual XPath notation

        # Storing extracted data in a dictionary
        item = {'quote_header': quote_header}

        # Yielding the item to be exported to CSV
        yield item


# Run the Spider and export data to CSV
process = CrawlerProcess(settings={
    'FEED_FORMAT': 'csv',
    'FEED_URI': 'first_scrape.csv'  # Corrected: added .csv extension
})
process.crawl(Spidey)
process.start()
