#  Origin-Destination data

Origin-destination (OD) data represents movement through geographic space, from an origin (O) to a destination (D). Sometimes also called "flow data," OD datasets contain details of trips between two geographic points or, more commonly, zones (which are often represented by a zone centroid).

Origin-destination flow data are common across many application areas in geography and are used to model many different types of movement processes, for example commuting, international migration, and urban transportation.  Recently, methods of network analysis have been applied successfully to analyze the structure of mobility flows inferred from cell phone data.

Example OD datasets are available from the U.S. Census Bureau [(LEHD Origin-Destination Employment Statistics)](https://lehd.ces.census.gov/data/#lodes) and Safegraph [(Neighborhood Patterns)](https://www.safegraph.com/neighborhood-patterns).

At a minimum, OD datasets include an origin ID, a destination ID, and a count of the number of trips that take place from the origin to the destination over a given time period.  Usually, the origin and destination IDs serve as keys to a table containing an arbitrary number of interesting attributes describing each place, e.g. geographical coordinates of its centroid, census characteristics, and footfall data.  Some but not all OD datasets also break down trip counts into collections of mutually exclusive, collectively exhaustive subgroups that can be analyzed separately, e.g. female and male, young and old, skilled and unskilled.

# Identifying and analyzing communities using origin-destination data

> **Source:** [A spatially aware method for mapping movement-based and place-based regions from spatial flow networks](https://onlinelibrary.wiley.com/doi/full/10.1111/tgis.12772). Transactions in GIS, 20 June 2021.
> **Source:** [NetworkX is a Python package for the creation, manipulation, and study of the structure, dynamics, and functions of complex networks](https://networkx.org/).

