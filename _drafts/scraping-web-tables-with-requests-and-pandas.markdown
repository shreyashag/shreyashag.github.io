---
title: Scraping web tables with requests and pandas
layout: post
time: 2018-08-04 21:46:40
categories: Web
---
Hey everyone,

It's been a long time since I posted something, I've been busy with work and other things.
I've written a lot of scrapes recently and while trying to reduce the code I would have to write, I stumbled upon something.

Have you heard on Pandas?

It's a fantastic library which not only is useful for maintaining data structures in it's famous Dataframe, but also helped me cut out BeautifulSoup (another awesome library which I used to use for web parsing) completely!

Now I just have to use requests and a one-liner from Pandas to read html tables.

Don't believe me?
Let's do this then!

Here's the website from which we want the data table.


import requests
import pandas

page = requests.get(url)
table_records = pandas.read_html(page.text, parse_dates=[''], id='').to_dict('records')

Yup, that's it!

print(item for item in table_records)

Here's the output.

If you noticed, there's a dateparser incorporated into the function call, that will automatically parse strified dates into a nice and convinient pandas Timestamp.

To get a python date object, we just need to call a .date() method on the Timestamp object.

Using this method has greatly cut down on the amount of time and code that would be used to scrape a similar table using BeautifulSoup.

Any comments? Ideas on how this could be even better? Hit me up on twitter @shreyash_ag!



