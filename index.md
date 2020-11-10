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
For some of these buckets the search is straightforward; for example, when searching for Trump there is only one word I'm interested in: Trump. But for some of the less-specific buckets, there are several keywords which could be included. The complete list of buckets/keywords is included in the code for this part of the analysis, available [here](https://github.com/grahamh39/DATS6103-Project-2-Graham-Hulsey-/blob/main/code/Graham%20Hulsey%20Project%202%20Code%20Part%202%20-%20Analysis.ipynb). After some data wrangling, it's time to make some plots and actually analyze all this data. All plots are available [here](https://github.com/grahamh39/DATS6103-Project-2-Graham-Hulsey-/tree/main/plots)

First, let's look at how frequently media outlets covered Trump and Biden. The following plots display that data. 

![trump](https://raw.githubusercontent.com/grahamh39/DATS6103-Project-2-Graham-Hulsey-/main/plots/trump_plot.png)
![biden](https://raw.githubusercontent.com/grahamh39/DATS6103-Project-2-Graham-Hulsey-/main/plots/biden_plot.png)

The first thing to notice is that Fox News covers Trump much more frequently than any others news outlet. The second thing to notice is that coverage of Biden was lower than coverage of Trump until Biden was announced as the president-elect the morning of November 7. This suggests that whether the news is good or bad, media outlets commit more space to covering Trump than they do other politicians.

Next, lets look at a couple of election-related buckets. The following graphs show election related headlines and headlines that concern the integrity of the election, respectively.

![election](https://raw.githubusercontent.com/grahamh39/DATS6103-Project-2-Graham-Hulsey-/main/plots/election_plot.png)
![integrity](https://raw.githubusercontent.com/grahamh39/DATS6103-Project-2-Graham-Hulsey-/main/plots/integrity_plot.png)

Across outlets, it seems that coverage of the election peaked on election night and has been slowly decreasing since. However, after election night there was a dramatic increase in headlines related to the integrity of the election on Fox. A few other outlets, such as the Washington Post, also covered the integrity of the election although not as frequently or consistently as Fox. Notablty, integrity related headlines don't really appear before election night, suggesting that the narrative that the election was "stolen" or "illegitimate" only formed after the results began to come in.

Now let's look at some non-election stories. First, the economy:

![economy](https://raw.githubusercontent.com/grahamh39/DATS6103-Project-2-Graham-Hulsey-/main/plots/economy_plot.png)

CNBC spends way more time on the economy than any other news network, with Fox coming in at a distant second. Most outlets spend very little time on the economy, though. Next, let's look at coverage of the COVID-19 pandemic:

![covid](https://raw.githubusercontent.com/grahamh39/DATS6103-Project-2-Graham-Hulsey-/main/plots/corona_plot.png)

Most news outlets have at least some coverage of the pandemic, and coverage seems nearly constant. This suggests that election-related events were not taking space away from pandemic coverage, implying that news organizations still felt that the pandemic was worth covering.

Lastly, let's see who is covering climate change and how frequently:

![climate](https://raw.githubusercontent.com/grahamh39/DATS6103-Project-2-Graham-Hulsey-/main/plots/climate_plot.png)

Not very surprising, unfortunately.

The last thing I want to do is look at what issues each outlet covers most. First, Fox News:

![fox](https://raw.githubusercontent.com/grahamh39/DATS6103-Project-2-Graham-Hulsey-/main/plots/fox_plot.png)

Fox largely covered 4 issues: the election, Trump, Biden, and coronavirus. Interestingly, Trump received more coverage than Biden until Biden was announced as the winner. 

Here is the New York Times:

![nyt](https://raw.githubusercontent.com/grahamh39/DATS6103-Project-2-Graham-Hulsey-/main/plots/ny_plot.png)

Just like Fox, the same 4 issues pop up: the election, Trump, Biden, and coronavirus. Unlike Fox, the Times gave Trump and Biden equal coverage until Biden won. 

Across all US-based media organizations, the same 4 stories were covered most frequently: the election, Trump, Biden, and coronavirus. However, among these issues each made different decisions as to which of the 4 stories to cover the most, and each reacted differently in response to election news.

Now, across foreign media outlets, we see a different story. Here is China Daily, an english-language news outlet run by the CCP:

![china](https://raw.githubusercontent.com/grahamh39/DATS6103-Project-2-Graham-Hulsey-/main/plots/china_plot.png)

There is some coverage of the election, but very little (and equal) coverage of Trump and Biden. This suggests that the CCP is aware of the US election but not particularly interested in who wins or loses. For comparison, here is Al-Jazeera:

![aj](https://raw.githubusercontent.com/grahamh39/DATS6103-Project-2-Graham-Hulsey-/main/plots/aj_plot.png)

Al-Jazeera devoted significant space to the election, and until Biden was announced as the winner, they devoted a lot more space to Trump. After Biden won, coverage of Trump dropped off while coverage of Biden soared. We can also see (small) coverage of different issues, such as the ongoing conflict between Azerbaijan and Armenia over the Nagorno-Karabakh region. This issue was mostly not covered by US outlets.

In sum, there is much to be learned from analyzing which news outlets choose to cover which stories. Web scraping in Python is a fantastic way to do that!
