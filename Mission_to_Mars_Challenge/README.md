# Mission-to-Mars

## Overview

The purpose of this analysis is to extract data and images from Mars websites using BeautifulSoup and Splinter, gather this data and store it in a Mongo database, then display this data using Flask. 

## Scrape the Mars Image and Titles

Visit the Mars website to scrape and create a distionary of the hemisphere image URL's.

```
def hemisphere(browser):
    # visit URL
    url = 'https://astrogeology.usgs.gov/search/results?q=hemisphere+enhanced&k1=target&v1=Mars'
    browser.visit(url)

    hemisphere_image_urls = []

    for i in range(4):
        hemispheres = {}
        #a) click on each hemisphere link
        browser.find_by_css('a.product-item img')[i].click()
        #b) navigate to the full-resolution image page
        #c) retrieve the full-resolution image URL string and title for the hemisphere image
        hemispheres['img_url'] = browser.find_by_text('Sample').first['href']
        hemispheres['title'] = browser.find_by_css('h2.title').text
        hemisphere_image_urls.append(hemispheres)
        #d) navigate back to the beginning to get the next hemisphere image
        browser.back()

    # Print the list that holds the dictionary of each image url and title.
    return(hemisphere_image_urls)
```

## Update Data Collected
Using Python and HTML, update the Mongo database and index.html file so the webpage contains all the information collected.

![image](https://user-images.githubusercontent.com/91445591/158075196-463387d1-2bb6-4eb4-837b-70e1ff222f98.png)


## Create URL

Create a URL using flask to visualize the data from scraping.py and index.html. 

![image](https://user-images.githubusercontent.com/91445591/158075505-1c09d2eb-3fe5-44a6-9832-d4d905577872.png)

## Summary

Using the tools provided, a script can be ran to automate the scraping of the requested data and visualize this data. 

![image](https://user-images.githubusercontent.com/91445591/158075568-ec924c45-78e0-49a8-8cf1-89c0dbfc40d7.png)
