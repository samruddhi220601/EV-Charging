# Interlinking EV Charging Infrastructure with Urban Fabric of California
## Samruddhi Purohit
## Command Line GIS

## Overview
This project examines EV infrastructure and its linkage to Orange County’s employment geography. It opens with a national-to-regional scan of cars-per-household at the census-tract level, then narrows to Orange County to analyze charger deployment year by year (2021–2024) using county-level datasets. While the source data distinguish Shared, Shared Private, Level 1, Level 2, and DC Fast chargers (useful for future, finer analysis), this phase aggregates to total chargers to establish the big picture. Building on research that finds a direct correlation between charger locations and commercial zones, the study specifically tests the relationship between EV chargers and office locations in Orange County. To assess practical access for commuters, we evaluate walkable catchments around office sites using 5-, 10-, and 15-minute buffers, highlighting where workplace-proximate charging may influence adoption, parking behavior, and last-mile choices.

## Data Sources
#### Cars per Household: 
Because the Census API was unavailable during the project timeline, data for vehicles per household at the census tract level for California were downloaded directly from the U.S. Census Bureau’s data portal. These tables originate from the ACS 5-year estimates (2019-2023) and include counts of households by number of vehicles available.

Several tracts along the California coastline contain no permanent housing (e.g., beaches or offshore water polygons). These areas naturally lack household-level vehicle data and therefore appear as missing. To avoid misinterpreting these geographic artifacts as data gaps, these non-residential coastal tracts are to be removed from the final visualization.

To compute cars per household, the total estimated number of vehicles was approximated by combining ACS categories (1 vehicle, 2 vehicles, and 3-or-more vehicles) and dividing this by the total number of occupied households. Because both the numerator and denominator have associated margins of error (MOEs), the reliability of this ratio cannot be evaluated by simply dividing standard errors or using a naïve propagation formula.

### EV Chargers per Population Density in California (2021-24) County Wise: 
The EV charger dataset used in this project was obtained from the California Energy Commission (energy.ca.gov), which provides statewide public and private charging infrastructure records. The raw dataset included stations from multiple years and formats, along with several partially reported 2025 entries. To ensure consistency, the dataset was cleaned by:

Removing incomplete or future-dated 2025 records

Dropping rows with missing geographic coordinates or essential charger attributes

Standardizing county names and charger attributes

To contextualize charging infrastructure across California, the cleaned EV charger dataset was joined with county-level population density data. This population dataset came from a county geodatabase containing area, population totals, and derived density measures. A shared county name field was used to merge the two datasets, enabling the creation of maps showing spatial patterns of charger concentration normalized by the underlying population distribution across counties. 

### EV Chargers Buffer in Irvine, California: 
This interactive map visualizes EV charging access relative to office locations using OpenStreetMap data obtained via OSMnx. The original dataset covered all of Orange County, but computing network-based walking isochrones for 5, 10, and 15 minutes around every office was slow. To keep analysis responsive while upholding policy relevance, the study zooms into Irvine. The reason for chooosing Irvine was its characteristic as an important highway-corridor having an employment cluster. This proved to be an ideal context to examine workplace-proximate charging.

The map consists of the following elements using lesson learnt from this class on Network Analysis and Geo-Processing tools. Walking-time buffers (5, 10, 15 min): Isochrones computed on the ‘walk’ network (not Euclidean circles), reflecting realistic pedestrian paths and barriers.

5-minute charging catchments: A dedicated layer showing 5-minute walk areas from EV charging stations to highlight near-term workplace access.

Point layers: Location pins for EV charging stations and office sites (both derived from OSMnx queries).

### Cars per Household in California (Census tracts, 2019-2023 ACS Data)
<img
  src="ca_cars_per_hh_fisherjenks_counties_quality.png"
  height="655" width="805">
  
### EV Chargers/Population Density
<iframe src="ev_chargers_popden_map.html" height ="555" width="1205"></iframe> You can explore this map [as its own web page here](ev_chargers_popden_map.html)

### Walking buffer from Office Locatios to Charging Stations, Irvine, CA
<iframe src="ev_chargers_office_map.html" height ="555" width="1205"></iframe> You can explore this map [as its own web page here](ev_chargers_office_map.html)

