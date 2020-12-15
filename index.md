Welcome! This is a brief synopsis of my Individual Project 3 for DATS 6103 Introduction to Data Mining. Python code for this project is available [here.](https://github.com/grahamh39/DATS6103-Proect-3-Graham-Hulsey/tree/main/code)

In this project, I conducted a network analysis of trade and security networks in four regions: the Middle East, Sub-Saharan Africa, East Asia, and the European Union member states. The first three region definitions come from the World Bank. Data on [bilateral trade](https://correlatesofwar.org/data-sets/bilateral-trade) and [defense cooperation agreements](https://correlatesofwar.org/data-sets/defense-cooperation-agreement-dataset) come from the Correlates of War Project.

Here, I'll just go over security networks. The gifs for trade data are too large to store on Github but can be viewed on Zenodo [here.](https://zenodo.org/record/4321990) To start, let's look at the European Union member states.

<img src="https://raw.githubusercontent.com/grahamh39/DATS6103-Proect-3-Graham-Hulsey/main/outputs/dca_European%20Union_all_years.gif" width="300" />

In this plot, and all subsequent plots, the size of the node is proportional to its [eigenvector centrality.](https://en.wikipedia.org/wiki/Centrality) If two countries have established a defense cooperation agreement, there is an edge connecting the two nodes (note that these networks are undirected). Average node conn

