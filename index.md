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
Here, sources is a dictionary of each news outlet and its url address, and all html text with the marker "a" gets appended to an empty list corresponding to that outlet in a dictionary. Some quick data cleaning turns this into a dataframe. I ran the web scraper once every morning and evening, beginning on the evening of November 2nd and ending on the evening of November 8. There were two occasions where the scraper had difficulty connecting to many newsites, the evening of November 4 (the night after the election) and the evening of November 7 (the night after Joe Biden was announced as the winner). The full jupyter notebook for this part of the analysis is available on my Github page [here](https://github.com/grahamh39/DATS6103-Project-2-Graham-Hulsey-/blob/main/code/Graham%20Hulsey%20Project%202%20Code%20Part%201%20-%20Web%20Scraping.ipynb).

Next, it's time for the analysis. The first thing I wanted to do was to see how much data I actually had. Since I'm interested in words, I counted the total number of words available. 
```
word_count_total = 0
for source in range(len(sources)):
    for date in range(len(dates)):
        text = df.iloc[source,date]
        word_count = len(text.split())
        word_count_total += word_count
print("Total word count is " + str(word_count_total))

Total word count is 171980
```
This loop goes through a dataframe containing the raw text, splits each cell one at a time, and adds the length of the resulting list to the word count. In total, there are 171,980 words in the data set. Obviously, I'm not interested in many of these, so I'll have to go through and just count the words I am interested in. To do that, I created an empty multi-indexed dataframe, where the columns are dates, and the rows are the news source (outer index) and the keyword bucket I am interested in. Here are the buckets of keywords I want to look for:

```
keywords = ["Trump","Biden","Election","Coronavirus","Election Integrity","Economy","Election Violence",
            "Azerbaijan/Armenia","Michigan","Wisconsin","Pennsylvania","Arizona","Nevada","Florida","Climate Change"]
```



