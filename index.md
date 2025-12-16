# Interlinking EV Charging Infrastructure with Urban Fabric of California
## Samruddhi Purohit
## Command Line GIS

## Overview
This project examines EV infrastructure and its linkage to Orange County’s employment geography. It opens with a national-to-regional scan of cars-per-household at the census-tract level, then narrows to Orange County to analyze charger deployment year by year (2021–2024) using county-level datasets. While the source data distinguish Shared, Shared Private, Level 1, Level 2, and DC Fast chargers (useful for future, finer analysis), this phase aggregates to total chargers to establish the big picture. Building on research that finds a direct correlation between charger locations and commercial zones, the study specifically tests the relationship between EV chargers and office locations in Orange County. To assess practical access for commuters, we evaluate walkable catchments around office sites using 5-, 10-, and 15-minute buffers, highlighting where workplace-proximate charging may influence adoption, parking behavior, and last-mile choices.

## Data Sources
1. Cars per Household: Because the Census API was unavailable during the project timeline, data for vehicles per household at the census tract level for California were downloaded directly from the U.S. Census Bureau’s data portal. These tables originate from the ACS 5-year estimates (2019-2023) and include counts of households by number of vehicles available.

Several tracts along the California coastline contain no permanent housing (e.g., beaches or offshore water polygons). These areas naturally lack household-level vehicle data and therefore appear as missing. To avoid misinterpreting these geographic artifacts as data gaps, these non-residential coastal tracts are to be removed from the final visualization.

To compute cars per household, the total estimated number of vehicles was approximated by combining ACS categories (1 vehicle, 2 vehicles, and 3-or-more vehicles) and dividing this by the total number of occupied households. Because both the numerator and denominator have associated margins of error (MOEs), the reliability of this ratio cannot be evaluated by simply dividing standard errors or using a naïve propagation formula.

2. Interactive Map: The EV charger dataset used in this project was obtained from the California Energy Commission (energy.ca.gov), which provides statewide public and private charging infrastructure records. The raw dataset included stations from multiple years and formats, along with several partially reported 2025 entries. To ensure consistency, the dataset was cleaned by:

Removing incomplete or future-dated 2025 records

Dropping rows with missing geographic coordinates or essential charger attributes

Standardizing county names and charger attributes

To contextualize charging infrastructure across California, the cleaned EV charger dataset was joined with county-level population density data. This population dataset came from a county geodatabase containing area, population totals, and derived density measures. A shared county name field was used to merge the two datasets, enabling the creation of maps showing spatial patterns of charger concentration normalized by the underlying population distribution across counties. 

3. EV Chargers Buffer in Orange County: To understand how accessible EV charging infrastructure is in Orange County, a 2-mile buffer was created around all public EV charging stations. This data was obtained using OSMnx and was filtered to ublic EV Charging Stations.

### Cars per Household in California (Census tracts, 2019-2023 ACS Data)
<img
  src="ca_cars_per_hh_fisherjenks_counties_quality.png"
  height="555" width="1005">
  
### EV Chargers/Population Density
<iframe src="ev_chargers_popden_map.html" height ="555" width="1205"></iframe> You can explore this map [as its own web page here](ev_chargers_popden_map.html)

### 2 mile Buffer for EV Charging Stations in Orange County
<img
  src="ev_chargers_orange_county.png"
  height="555" width="1605">
