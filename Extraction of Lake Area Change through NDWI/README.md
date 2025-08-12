# Area Change Detection Tool

This script uses **Google Earth Engine (GEE)** and **geemap** to calculate area changes between two different years for a selected region.

## What It Does
- Lets you draw a region of interest on a map.
- Lets you choose start and end years.
- Optionally removes clouds from images.
- Calculates the change in area (in sq.km) between the two years.

## Requirements
- Python 3.x
- geemap
- earthengine-api
- ipywidgets

Install with:
```bash
pip install geemap earthengine-api ipywidgets
