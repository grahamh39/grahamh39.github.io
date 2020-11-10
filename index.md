Welcome! This is a presentation of my Individual Project 2 for DATS 6103 Introduction to Data Mining.

In this project, I chose to gather data on headlines posted to major news sites and to analyze them in light of the ongoing US presidential election. I chose 12 news outlets:

1. [New York Times](https://www.nytimes.com/)
2. [Washington Post](https://www.washingtonpost.com/)
3. [CNBC](https://www.cnbc.com)
4. [Al-Jazeera](https://www.aljazeera.com/)
5. [BBC](https://bbc.com/news)
6. [China Daily](https://global.chinadaily.com.cn/)
7. [Fox News](https://www.foxnews.com/)
8. [Mehr News](https://en.mehrnews.com/)
9. [The Atlantic](https://www.theatlantic.com/)
10. [Buzzfeed](https://www.buzzfeed.com/)
11. [New Yoker](https://www.newyorker.com/)
12. [Mother Jones](https://www.motherjones.com/)

These outlets represent a variety of ideological and geographic viewpoints, and they will make for interesting analysis.

The first step is to actually go and scrape the data from the websites. Each news organization has their own unique web page setup, but all news sites make their headlines links (so that users can click on a headline and be taken to the story). After getting everything set up, the code to actually scrape the websites is fairly straightforward:

```
for key in sources:
    source_url = sources[key]
    sauce = url.urlopen(source_url).read()
    soup = BeautifulSoup(sauce, 'html5lib')
    for paragraph in soup.find_all("a"):
        scrapes[key].append(paragraph.text)
```
Here, sources is a dictionary of each news outlet and its url address, and all html tet with the marker "a" gets appended to an empty list in a dictionary. Some quick data cleaning turns this into a dataframe. I ran the web scraper once every morning and evening, beginning on the evening of November 2nd and ending on the evening of November 8. There were two occasions where the scraper had difficulty connecting to many newsites, the evening of November 4 (the night after the election) and the evening of November 7 (the night after Joe Biden was announced as the winner).
