---
categories: Web
date: "2018-08-05T00:00:00Z"
time: "2018-08-05 04:13:45"
title: Scraping web tables with requests and pandas
---
Hey everyone,

It's been a long time since I posted something, I've been busy with work and other things.
I've written a lot of scrapes recently and while trying to reduce the code I would have to write, I stumbled upon something.

Have you heard about [Pandas](https://pandas.pydata.org/)

It's a fantastic library which not only is useful for maintaining data structures in it's famous Dataframe, but also helped me cut out BeautifulSoup (another awesome library which I used to use for web parsing) completely!

Now I just have to use requests and a one-liner from Pandas to read html tables.

Don't believe me?
Let's do this then!

Here's the website from which we want the data table.<br/>
[W3 Schools HTML Tables](https://www.w3schools.com/html/html_tables.asp)


And this is how we can convert the web html table into a usable list of python dictionaries-


```python
import requests
import pandas

page = requests.get('https://www.w3schools.com/html/html_tables.asp')
table_records = pandas.read_html(url, parse_dates=[''], id='customers')[0].to_dict('records')
```

Yup, that's it!

```python
print(*table_records, sep='\n')
```

Here's the output.


``` bash
{'Company': 'Alfreds Futterkiste', 'Contact': 'Maria Anders', 'Country': 'Germany'}
{'Company': 'Centro comercial Moctezuma', 'Contact': 'Francisco Chang', 'Country': 'Mexico'}
{'Company': 'Ernst Handel', 'Contact': 'Roland Mendel', 'Country': 'Austria'}
{'Company': 'Island Trading', 'Contact': 'Helen Bennett', 'Country': 'UK'}
{'Company': 'Laughing Bacchus Winecellars', 'Contact': 'Yoshi Tannamuri', 'Country': 'Canada'}
{'Company': 'Magazzini Alimentari Riuniti', 'Contact': 'Giovanni Rovelli', 'Country': 'Italy'}

```
If you noticed, there's a dateparser incorporated into the function call, that will automatically parse strified dates into a nice and convinient pandas Timestamp.

To get a python date object, we just need to call a .date() method on the Timestamp object.

Here is a clearer use of this with a function call -


```python
import requests
import pandas


def read_html_table(url, table_id):
    response = requests.get(url=url)
    table_records = pandas.read_html(io=response.text, header=0, attrs={
        'id': table_id})[0].to_dict('records')
    return table_records


if __name__ == "__main__":
    url = 'https://www.w3schools.com/html/html_tables.asp'
    id = 'customers'
    table_records = read_html_table(url=url, table_id=id)
    print(*table_records, sep='\n')

```

Using this method has greatly cut down on the amount of time and code that would be used to scrape a similar table using BeautifulSoup.

Any comments? Ideas on how this could be even better? Hit me up on twitter @shreyash_ag!



