\#  Satellite Image Area Change Detection Tool



This project provides a Python-based tool for \*\*calculating area changes between two satellite images\*\* using \*\*Google Earth Engine (GEE)\*\* and \*\*geemap\*\*.  

It allows users to input a region of interest (ROI), specify a time range, and compute \*\*change in surface area\*\* between two different years.



---



\## Features

\- Load and display satellite images via \*\*Google Earth Engine\*\*.

\- User-friendly polygon drawing tool to select an ROI.

\- Interactive prompts for start/end years and change detection.

\- Calculates \*\*area difference\*\* in square kilometers between two selected years.

\- Outputs the calculated change in a clear, readable format.



---



\## Requirements

\- Python 3.x

\- \[geemap](https://geemap.org/)

\- \[ee](https://developers.google.com/earth-engine)

\- ipywidgets



Install required packages:

```bash

pip install geemap earthengine-api ipywidgets



