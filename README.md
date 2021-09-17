# Spatial-Flow Network Analysis

A spatial-flow network is a mathematical model of the movement of matter through geographic space from origins to destinations.

Communication networks, social networks, trade networks et al each take their names from the kind of matter that moves through them.

While techniques for spatial-flow network analysis are not new, the widespread availability of large spatial-flow network datasets is more recent.

Large spatial-flow network datasets are available from the U.S. Census Bureau [(LEHD Origin-Destination Employment Statistics)](https://lehd.ces.census.gov/data/#lodes) and Safegraph [(Neighborhood Patterns)](https://www.safegraph.com/neighborhood-patterns) for free.

# Identifying and analyzing communities in a spatial-flow network model of DC-Baltimore commuting data 

> **Source:** [CDLIB: A python library to extract, compare and evaluate communities from complex networks](https://doi.org/10.1007/s41109-019-0165-9). Applied Network Science, 2019.

> **Source:** [A spatially aware method for mapping movement-based and place-based regions from spatial flow networks](https://onlinelibrary.wiley.com/doi/full/10.1111/tgis.12772). Sebastijan Sekulic, Jed Long and Urska Demsar. Transactions in GIS, 20 June 2021.

> **Source:** [NetworkX](https://networkx.org/) is a Python package for the creation, manipulation, and study of the structure, dynamics, and functions of complex networks.

In network science, a community is a collection of nodes (or edges) that are more closely related to each other than to the other nodes (or edges) in the graph.

The python library CDLIB offers easy and standardized access to methods for identifying and analyzing communities in a dataset.  

We use CDLIB to implement the community detection technique of Sekulic, Long, and Demsar (2021) on DC-Baltimore commuting data extracted from the U.S. Census Bureau's 2018 LEHD Origin-Destination Employment Statistics release.  

The data consists of 372,634 undirected edges, each connecting two census blocks from among the 63,728 that house or host a commuting worker--one in the Washington-Arlington-Alexandria, DC-VA-MD-WV Metropolitan Statistical Area (MSA) and the other in the Baltimore-Columbia-Towson, MD MSA.  On average, 30.2 miles separate the census block pairs.

In 2018, there were 172,500 DC-based Baltimore commuters and 213,491 Baltimore-based DC commuters in the region.  Our analysis uncovers 5,796 non-trivial communities (i.e. communities with more than three edges), the largest of these consisting of 4,962 edges.  On average, non-trivial communities contain 18 edges.

# Preliminary Observations
Here is a basemap of the DC-Baltimore region, displayed on a Leaflet map via [folium](http://python-visualization.github.io/folium/).
![](https://i.ibb.co/T2wBSpN/basemap.png)

A community is a collection of nodes (or edges) that are more closely related to each other than to the other nodes (or edges) in the graph.  Such a collection can be mapped in any number of ways, depending on the question of interest.  

In what follows, we find it useful to visualize a community as (1) a union of census block polygon geometries, (2) a convex hull of census block centroids, and (3) a bounding box of the convex hull of census block centroids.  

Each representation is shown below for a randomly-selected reference community which happens to consist of 15 commuting workers, each housed or hosted in one of 6 census blocks (nodes) that are connected by 5 distinct paths (edges).

* Polygon Union

![](https://i.ibb.co/KNdBwM5/basemap-blocks.png)

Census blocks are statistical areas bounded by visible features such as roads, streams, and railroad tracks, and by nonvisible boundaries such as property lines, city, township, school district, county limits and short line-of-sight extensions of roads.  They are generally small in size (as small as 30,000 square feet).  In remote areas, however, census blocks may encompass hundreds of square miles.

For readability, the census block centroids of the reference community have been tagged here with markers.  The largest census block in this community--located a few miles northeast of Columbia, MD-- is just barely visible, in red, at the base of its marker. 
 
* Convex Hull

![](https://i.ibb.co/fNtb3GX/basemap-convexhull.png)

The convex hull is best thought of as the shape enclosed by a rubber band stretched around the census block centroids. 

* Bounding Box

![](https://i.ibb.co/pWkrbJc/basemap-envelope.png)

The bounding box is the smallest rectangle that can enclose the convex hull.

# Characterizing Patterns of Movement in a Community

A community is a collection of nodes (or edges) that are more closely related to each other than to the other nodes (or edges) in the graph.

Recently, planners have started to apply the network science concept of community to the problem of identifying "travel-to-work areas," spatially contiguous regions in which labor supply and demand are equal.
  
We are interested in distinguishing travel-to-work areas in the DC-Baltimore region, first according to their patterns of movement and second according to the socioeconomic characterisitics of the workers who belong to them.

## Characterizing Patterns of Movement in a Community

Sekulic, Long, and Demsar (2021) offer a number of statistics for characterizing patterns of movement in a community.  Many of these are derived from the distribution of a community's edge bearings, which quantify the directional relationship between any two nodes connected by an edge.  
![](https://i.ibb.co/6w91qsn/bearing.png)

If the standard deviation of the distribution of edge bearings is small, all of that community's edges point in roughly the same direction.  Sekulic, Long, and Demsar (2021) use this fact to distinguish directionally homogenous "movement-based" communities from "place-based" communities where there is no specific direction to the movements.

Since we deliberatley have chosen to analyze edges that connect DC-based nodes to Baltimore-based nodes, the communities we study are generally movement-based and the corresponding range of edge standard deviations is small.

In fact, among the 5,796 non-trivial communities, the smallest bearing standard deviation is 0.01 and the largest is 1.76.  Both measurements indicate communities with a slender convex hull, as shown below in Figures 1 and 2, respectively.  (Our reference community has a bearing standard deviation of 0.27.)

![](https://i.ibb.co/WcGhXyW/minBsd.png)
Figure 1.

![](https://i.ibb.co/GWJtRDX/maxBsd.png)
Figure 2.

Another set of useful statistics are derived from the convex hull.  These include the area, which quantifies the magnitude of movement overall, and the bounding box elongation, which is the ratio between its longest and shortest sides.

As mentioned, the origin-destination pairs we study are in different metropolitan regions, separated by a distance of 30 miles on average.  The corresponding convex hulls, therefore, generally have areas on the order of hundreds of square miles.

Among the 5,796 non-trivial communities, the smallest convex hull has an area of 10.5 square miles, while the the largest convex hull has an area of 7469.8 square miles.

To see better the relationship between convex hull and elongation, note that the convex hull shown in Figure 1 has an area of 13.7 square miles and an elongation of 1.56, while the convex hull shown in Figure 2 has an area of 340.7 square miles and an elongation of 8.15.

The larger convex hull in Figure 2 is obvious, but its large elongation stems not from size but from a substantially vertical orientation relative to the coordinate axes.

By comparision, our reference community has an area of 167 square miles.  Its substantially diagonal orientation relative to the coordinate axes yields an elongation of 2.14, more comparable to the elongation of the convex hull shown in Figure 1, which also has a diagonal orientation.  

## Characterizing Socioeconomic Characteristics of a Community
Given our focus on movement-based communities, it is more interesting to study the people that make them up.

The DC-Baltimore communiting data contains demographic detail on the workers who reside or work in census blocks connected by a specific employment and housing arrangement.  For instance, we can learn about the age, earnings and industry sectors of the 15 workers in our reference community.

--- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Census Block (O) | Census Block (D) | Total Number of Workers | 29 or younger | 30 to 54 | 55 or older | $1250/month or less | $1251 to $3333 | more than $3333/month | goods producing | trade, transportation and utilities | all other services|
--- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
240276011042007 | 240338072002022 | 2 | 0 | 2 | 0 | 2 | 0 | 0 | 0 | 0 | 2 | 
240276011042007 | 240317009012008 | 2 | 0 | 1 | 1 | 0 | 1 | 1 | 0 | 0 | 2 | 
240276011042007 | 240338072001001 | 6 | 3 | 3 | 0 | 1 | 3 | 2 | 0 | 0 | 6 | 
240276011042007 | 240317050004029 | 1 | 0 | 1 | 0 | 0 | 0 | 1 | 0 | 0 | 1 | 
240276011042007 | 240317060131014 | 4 | 0 | 3 | 1 | 0 | 0 | 4 | 0 | 0 | 4 | 
 |  |  |  |  |  |  |  |  |  |  |  |
| | TOTALS | 15 | 3 | 10 | 2 | 3 | 4 | 8 | 0 | 0 | 15 |

The workers in our reference community are high-wage service industry workers in their prime working years.
  
Although our labeling of the census blocks as "O" and "D" would appear to imply that all 15 workers reside in the same census block and work in different census blocks, this is not necessarily the case; the network edges are undirected.  Without further examination we can't know with certainty whether the commuting workers in this particular commmunity reside or work in the same census block.