# Wildfire Analysis Tool

A Python tool for analysing and visualising wildfire impacts by county across US states.

## Overview

This script fetches wildfire perimeter data and county boundaries from ArcGIS REST services, then calculates and visualises the burnt area within each county for a specified state. It produces both tabular data (CSV) and visualisation maps (PNG).

## Features

- Fetches county boundary data for any US state
- Retrieves current year-to-date wildfire perimeter data
- Calculates burnt area by county using spatial analysis
- Generates CSV reports with burnt area statistics
- Creates maps highlighting the most affected counties
- Handles large datasets through batched API requests

## Requirements

```python
pip install requests geopandas pandas matplotlib
```

## Usage

1. Set the state name in the script:
   ```python
   state_name = "Alabama"
   ```

2. Run the script:
   ```python
   python pyscript2.py
   ```

3. Output files:
   - `burnt_area_by_county_[STATE_NAME].csv`: Tabular data showing burnt area by county
   - `burnt_area_map_[STATE_NAME].png`: Visualization map of the burnt areas

## How It Works

The script performs the following steps:

1. Fetches county boundaries for the specified state
2. Retrieves wildfire perimeter data for the current year
3. Performs spatial intersection to calculate burnt area by county
4. Generates a sorted report of counties by burnt area
5. Creates a choropleth map highlighting the most affected areas

## Functions

- `get_counties_for_state(state_name)`: Retrieves county boundaries for a specific state
- `get_fire_perimeters()`: Fetches wildfire perimeter data in batches
- `calculate_burnt_area_by_county(counties_gdf, fires_gdf)`: Performs spatial analysis to calculate burnt area
- `summarise_burnt_area_for_state(state_name)`: Coordinates the analysis workflow
- `create_burnt_area_map(results_df, counties_gdf, state_name)`: Generates visualisation maps

## Data Sources

This tool uses ArcGIS REST services:
- County boundaries: USA Counties Generalised Boundaries
- Fire perimeters: WFIGS Interagency Perimeters Year-To-Date

## Example Output

For a state analysis, you'll get:
- A CSV file with each county and its burnt area in acres
- A map visualizing the burnt areas with the top 5 most affected counties labeled

## Notes

- The script handles coordinate system conversions automatically
- Large fire datasets are retrieved in batches of 2000 features
- All counties are shown on the map, even those with no burnt area
# Wildfire Burnt Area Analysis Tool

## Overview
This tool analyses the burnt areas caused by wildfires in a specific state in the USA. It retrieves county boundaries and fire perimeter data from external APIs, calculates the extent of burnt areas per county, and generates both tabular and visual outputs to aid in understanding wildfire impacts.

## Features
- Retrieves county boundaries for any selected US state
- Fetches comprehensive fire perimeter data from official sources
- Calculates burnt area statistics by county using spatial analysis
- Generates summary CSV files of burnt area by county
- Creates visualisation maps highlighting the most affected counties

## Installation

### Requirements
To run this tool, you will need Python 3.12 and several dependencies. You can set up your environment using the provided `environment.yml` file:

```bash
# Clone the repository
git clone https://github.com/msainty8/EGM722_Michael_Sainty_Assignment_2.git
cd EGM722_Michael_Sainty_Assignment_2-main

# Create a conda environment from the environment.yml file
conda env create -f environment.yml

# Activate the environment 
conda activate egm722_assignment
```

### Dependencies
The main packages required are:
- requests
- geopandas
- pandas
- matplotlib

## Usage
To run the analysis, simply execute the main Python script and specify a state name:

```python
# At the bottom of the script, change the state name to analyse a different state
state_name = "California"  # Replace with your state of interest

# Run the analysis
burnt_area_df, counties_gdf = summarise_burnt_area_for_state(state_name)

# Display the pandas table
print(burnt_area_df)

# Create a map showing burnt area by county
create_burnt_area_map(burnt_area_df, counties_gdf, state_name)
```

## Outputs
The tool generates two main outputs:
1. A CSV file named `burnt_area_by_county_[STATE_NAME].csv` containing tabular data of burnt areas by county
2. A map visualisation saved as `burnt_area_map_[STATE_NAME].png` showing the spatial distribution of burnt areas

## Data Sources
This tool uses the following data sources:
- County boundaries: ArcGIS REST service (USA Counties Generalized Boundaries)
- Fire perimeters: WFIGS Interagency Perimeters YearToDate service

## Licence
This project is licensed under the [MIT License](https://github.com/msainty8/EGM722_Michael_Sainty_Assignment_2/blob/main/LICENSE).