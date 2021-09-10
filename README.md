# Spatial-Flow Network Analysis

A spatial-flow network is a mathematical model of the movement of matter through geographic space from an origin (O) to a destination (D).

Communication, social, and trade networks each take their names from the kind of matter that moves through them.

While techniques for spatial-flow network analysis are not new, the widespread availability of large spatial-flow network datasets is more recent.

Large spatial-flow network datasets are available from the U.S. Census Bureau [(LEHD Origin-Destination Employment Statistics)](https://lehd.ces.census.gov/data/#lodes) and Safegraph [(Neighborhood Patterns)](https://www.safegraph.com/neighborhood-patterns) for free.

# Identifying and analyzing communities in a spatial-flow network model of DC-Baltimore commuting data 

> **Source:** [CDLIB: A python library to extract, compare and evaluate communities from complex networks](https://doi.org/10.1007/s41109-019-0165-9). Applied Network Science, 2019.

> **Source:** [A spatially aware method for mapping movement-based and place-based regions from spatial flow networks](https://onlinelibrary.wiley.com/doi/full/10.1111/tgis.12772). Sebastijan Sekulic, Jed Long and Urska Demsar. Transactions in GIS, 20 June 2021.

> **Source:** [NetworkX](https://networkx.org/) is a Python package for the creation, manipulation, and study of the structure, dynamics, and functions of complex networks.

In network science, a community is a collection of nodes (or edges) that are more closely related to each other than to the other nodes (or edges) in the graph.

The python library CDLIB offers easy and standardized access to methods for identifying and analyzing communities in a dataset.  

We use CDLIB to implement the community detection technique of Sekulic, Long, and Demsar (2021) on DC-Baltimore commuting data extracted from the U.S. Census Bureau's 2018 LEHD Origin-Destination Employment Statistics release.  

The data consists of 372,634 undirected edges, each connecting two census blocks that house and host a commuting worker--one in the Washington-Arlington-Alexandria, DC-VA-MD-WV Metropolitan Statistical Area (MSA) and the other in the Baltimore-Columbia-Towson, MD MSA.  On average, 30.2 miles separate the census block pairs, and there are 63,728 census blocks in the region that house or host a commuting worker.  

In 2018, there were 172,500 DC-based Baltimore commuters and 213,491 Baltimore-based DC commuters in the region.  Our analysis uncovers 5,796 non-trivial travel-to-work areas (i.e. communities with more than three edges) with the largest of these consisting of 4,962 edges.  On average, non-trivial travel-to-work areas contain 18 edges.

# Preliminary Observations
Here is a basemap of the DC-Baltimore region, displayed on a Leaflet map via folium.
![](https://i.ibb.co/T2wBSpN/basemap.png)

A community is a collection of nodes (or edges) that are more closely related to each other than to the other nodes (or edges) in the graph.  Such a collection can be mapped in any number of ways, depending on the question of interest.  

In what follows, we find it useful to present a community as (1) a union of census block polygon geometries, (2) a convex hull of census block centroids, and (3) a bounding box of the convex hull of census block centroids.  

Each representation is shown below for a reference community which happens to consist of 15 commuting workers, each housed or hosted in one of 6 census blocks (nodes) that are connected by 5 distinct paths (edges).

* Polygon Union

![](https://i.ibb.co/KNdBwM5/basemap-blocks.png)

Census blocks are statistical areas bounded by visible features such as roads, streams, and railroad tracks, and by nonvisible boundaries such as property lines, city, township, school district, county limits and short line-of-sight extensions of roads.  They are generally small in size, as small as 30,000 square feet.  In remote areas, however, census blocks may encompass hundreds of square miles.

For readability, the census block centroids have been tagged with markers.
 
* Convex Hull

![](https://i.ibb.co/fNtb3GX/basemap-convexhull.png)

The convex hull may be visualized as the shape enclosed by a rubber band stretched around the census block centroids. 

* Bounding Box

![](https://i.ibb.co/pWkrbJc/basemap-envelope.png)

The bounding box is the smallest rectangle within which all the points in the convex hull lie.

# Characterizing Patterns of Movement in a Community

A community is a collection of nodes (or edges) that are more closely related to each other than to the other nodes (or edges) in the graph.

In the DC-Baltimore commuting data, communities can be interpreted as "travel-to-work areas" in the DC-Baltimore region.

We are interested in distinguishing these communities, first according to the patterns of movement and second according to the socioeconomic characterisitics of the workers who belong to them.

## Characterizing Patterns of Movement in a Community

Sekulic, Long, and Demsar (2021) offer a number of statistics for characterizing patterns of movement in a community.  We illustrate each of them below.

### Standard Deviation of Flow Bearings
The standard deviation of the bearings of all flows in a spatial-flow network community identifies the level of directional homogeneity in those flows.  

Our reference community has a bearing standard deviation of 0.27.

Among the 5,796 non-trivial communities, the smallest bearing standard deviation is 0.01 and the largest is 1.76.

A small bearing standard deviation indicates that the flows in that community move in roughly the same direction.
![](https://i.ibb.co/rckD59x/minBsd.png)
![](https://i.ibb.co/wr9k2pY/maxBsd.png)

### Kurtosis of Flow Bearings
The kurtosis of the bearings of all flows in a spatial-flow network community identifies concentrated movement in a single direction.  A small bearing kurtosis indicates that the distribution of bearings is peaked around its average, with very few observations in the tails.

Our reference community has a bearing kurtosis of -1.52.

Among the 5,796 non-trivial communities, the smallest bearing kurtosis is -2.00 and the largest is 25.61.

![](https://i.ibb.co/L9WRrDW/minBkt.png)
![](https://i.ibb.co/5jPxMGG/maxBkt.png)

### Convex Hull Area and Elongation 



## Characterizing Socioeconomic Characteristics of a Community