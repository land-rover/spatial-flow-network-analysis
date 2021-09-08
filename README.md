# Spatial-Flow Network Analysis

A spatial-flow network is a mathematical model of the movement of matter through geographic space from an origin (O) to a destination (D).

Communication, social, and trade networks each take their names from the kind of matter moved through them.

While techniques for spatial-flow network analysis are not new, the widespread availability of large spatial-flow network datasets is new.

Large spatial-flow network datasets are available from the U.S. Census Bureau [(LEHD Origin-Destination Employment Statistics)](https://lehd.ces.census.gov/data/#lodes) and Safegraph [(Neighborhood Patterns)](https://www.safegraph.com/neighborhood-patterns) for free.

# Identifying and analyzing communities in a spatial-flow network of DC-Baltimore commuting data 

> **Source:** [CDLIB: A python library to extract, compare and evaluate communities from complex networks](https://doi.org/10.1007/s41109-019-0165-9). Applied Network Science, 2019.

> **Source:** [A spatially aware method for mapping movement-based and place-based regions from spatial flow networks](https://onlinelibrary.wiley.com/doi/full/10.1111/tgis.12772). Sebastijan Sekulic, Jed Long and Urska Demsar. Transactions in GIS, 20 June 2021.

> **Source:** [NetworkX](https://networkx.org/) is a Python package for the creation, manipulation, and study of the structure, dynamics, and functions of complex networks.

In network science, a community is a collection of nodes (or edges) that are more closely related to each other than to the other nodes (or edges) in the graph.

The python library CDLIB offers easy and standardized access to methods for identifying and analyzing communities in a dataset.  

Following Sekulic, Long, and Demsar (2021), we use DC-Baltimore commuting data extracted from the U.S. Census Bureau's 2018 LEHD Origin-Destination Employment Statistics release to identify travel-to-work areas in that region.  

The data consists of 372,634 undirected edges, each connecting two census blocks that house and host a commuting worker--one in the Washington-Arlington-Alexandria, DC-VA-MD-WV Metropolitan Statistical Area (MSA) and the other in the Baltimore-Columbia-Towson, MD MSA.  On average, 30.2 miles separate the census block pairs, and there are 63,728 census blocks in the region total.  

In 2018, there were 172,500 DC-based Baltimore commuters and 213,491 Baltimore-based DC commuters in the region.  Our analysis uncovers 5,796 non-trivial travel-to-work areas (i.e. communities with more than three edges) with the largest of these consisting of 4,962 edges.  On average, non-trivial travel-to-work areas contain 18 edges.

Here is a basemap of the DC-Baltimore region, displayed on a Leaflet map via folium.
![](https://ibb.co/8smDpTQ).
# Questions and Answers
