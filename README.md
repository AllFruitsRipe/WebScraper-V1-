# Sample codeV1
import scrapy
from scrapy.crawler import CrawlerProcess


class Spidey(scrapy.Spider):
    name = "Spidey"

    def start_requests(self):
        url = 'INSERT URL'
        yield scrapy.Request(url=url, callback=self.parse_one)

    def parse_one(self, response):
        # Extracting data from the webpage
        quote_header = response.xpath('XPATH NOTATION').getall()



        # Storing extracted data in a dictionary
        item = {'quote_header': quote_header}

        # Yielding the item to be exported to CSV
        yield item


 Run the Spider and export data to CSV
process = CrawlerProcess(settings={
    'FEED_FORMAT': 'csv',
    'FEED_URI': 'first_scrape.csv'  # Corrected: added .csv extension
})
process.crawl(Spidey)
process.start()
