#  Spatially-Referenced Origin-Destination Data

Spatially-Referenced Origin-destination (OD) data represents movement through geographic space, from an origin (O) to a destination (D). Sometimes also called "flow data," OD datasets contain details of trips between two geographic points or, more commonly, zones (which are often represented by a zone centroid).

Origin-destination flow data are common across many application areas in geography and are used to model many different types of movement processes, for example commuting, migration, and trade.  Recently, methods of network analysis have been applied successfully to analyze the structure of mobility flows inferred from cell phone data.

Example OD datasets are available from the U.S. Census Bureau [(LEHD Origin-Destination Employment Statistics)](https://lehd.ces.census.gov/data/#lodes) and Safegraph [(Neighborhood Patterns)](https://www.safegraph.com/neighborhood-patterns).

At a minimum, OD datasets include an origin ID, a destination ID, and a count of the number of trips that take place from the origin to the destination over a given time period.  Usually, the origin and destination IDs serve as keys to a table containing an arbitrary number of interesting attributes describing each place, e.g. geographical coordinates of its centroid, census characteristics, and footfall data.  Some but not all OD datasets also break down trip counts into collections of mutually exclusive, collectively exhaustive subgroups that can be analyzed separately, e.g. female and male, young and old, skilled and unskilled.

# Identifying and analyzing communities using spatially-referenced origin-destination data

> **Source:** [A spatially aware method for mapping movement-based and place-based regions from spatial flow networks](https://onlinelibrary.wiley.com/doi/full/10.1111/tgis.12772). Sebastijan Sekulic, Jed Long and Urska Demsar. Transactions in GIS, 20 June 2021.

> **Source:** [NetworkX](https://networkx.org/) is a Python package for the creation, manipulation, and study of the structure, dynamics, and functions of complex networks.

> **Source:** [CDLIB: A python library to extract, compare and evaluate communities from complex networks](https://doi.org/10.1007/s41109-019-0165-9). Applied Network Science, 2019.

In network science, a community is a collection of nodes (or edges) that are more closely related to each other than to the other nodes (or edges) in the graph.

The python library CDLIB offers easy and standardized access to methods for identifying and analyzing communities in a dataset.  

Following Sekulic, Long, and Demsar (2021), we use DC-Baltimore commuting data extracted from the U.S. Census Bureau's 2018 LEHD Origin-Destination Employment Statistics release to identify travel-to-work areas in that region.  The data consists of 372,634 undirected edges, each connecting two census blocks that house and host a commuting worker--one in the Washington-Arlington-Alexandria, DC-VA-MD-WV Metropolitan Statistical Area (MSA) and the other in the Baltimore-Columbia-Towson, MD MSA.  On average, 30.2 miles separate the census block pairs, and there are 63,728 census blocks in the region.  

In 2018, there were 172,500 DC-based Baltimore commuters and 213,491 Baltimore-based DC commuters in the region.  Our analysis uncovers 7,742 non-trivial travel-to-work areas, i.e. communities consisting of three or more edges, with the largest of these consisting of 4,962 edges.