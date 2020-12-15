Welcome! This is a brief synopsis of my Individual Project 3 for DATS 6103 Introduction to Data Mining. Python code for this project is available [here.](https://github.com/grahamh39/DATS6103-Proect-3-Graham-Hulsey/tree/main/code)

In this project, I conducted a network analysis of trade and security networks in four regions: the Middle East, Sub-Saharan Africa, East Asia, and the European Union member states. The first three region definitions come from the World Bank. Data on [bilateral trade](https://correlatesofwar.org/data-sets/bilateral-trade) and [defense cooperation agreements](https://correlatesofwar.org/data-sets/defense-cooperation-agreement-dataset) come from the Correlates of War Project.

Here, I'll just go over security networks. The gifs for trade data are too large to store on Github but can be viewed on Zenodo [here.](https://zenodo.org/record/4321990) To start, let's look at the European Union member states.

<img src="https://raw.githubusercontent.com/grahamh39/DATS6103-Proect-3-Graham-Hulsey/main/outputs/dca_European%20Union_all_years.gif" />

In this plot, and all subsequent plots, the size of the node is proportional to its [eigenvector centrality.](https://en.wikipedia.org/wiki/Centrality) If two countries have established a defense cooperation agreement, there is an edge connecting the two nodes (note that these networks are undirected). Average node connectivity, or the average percent of nodes connected to each other, approaches 30% by 2010. Notably, most defense cooperation agreements were signed after the creation of the European Union, suggesting increased economic connectivity can lead to increased security connectivity.

Next up is East Asia. China's rise is the most important event in East Asia over the past 30 years, but that is not reflected in the network of regional defense cooperation agreements. 

<img src="https://raw.githubusercontent.com/grahamh39/DATS6103-Proect-3-Graham-Hulsey/main/outputs/dca_East%20Asia_all_years.gif" />

Japan, Australia, Vietnam, and Singapore emerge as the most important countries in the region, as measured by eigenvector centrality. Also of note, East Asia is less connected by defense cooperation agreements than the EU- average node connectivity is less than 1%. One way conflicts can spiral out of control occurs when networks of alliances are triggered, drawing several countries into a conflict. Alliances can creaate deterrence, but can also increase the probability of large regional wars.

Lastly, let's take a look at the Middle East.

<img src="https://raw.githubusercontent.com/grahamh39/DATS6103-Proect-3-Graham-Hulsey/main/outputs/dca_Middle%20East_all_years.gif" />

