# Data-to-CSV
import csv
from urllib.request import urlopen
from bs4 import BeautifulSoup
html = urlopen('https://en.wikipedia.org/wiki/Comparison_of_text_editors')
bs = BeautifulSoup(html, 'html.parser')
table = bs.findAll('table', {'class': 'wikitable'})[0]
rows = table.findAll('tr')
csvFile = open('Text-Editor-Data.csv', 'wt+')
writer = csv.writer(csvFile)
try:
    for row in rows:
        csvRow = []
        for cell in row.findAll(['td', 'th']):
            csvRow.append(cell.get_text())
            writer.writerow(csvRow)
finally:
    csvFile.close()

    Save Scraped Data to CSV
Now that we know how to scrape a website with Python, let’s look at how to save the scraped data to a CSV file.

CSV files are a common format for storing tabular data, and they can be easily read and manipulated with a spreadsheet program like Microsoft Excel or Google Sheets.

To save scraped data to a CSV file in Python, we’ll use the built-in CSV module.

Let’s take an example that scrapes the title and URL of the top 10 Google search results for a given query and saves the results to a CSV file:
