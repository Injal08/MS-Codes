# NetCDF/GRIB/HDF to CSV Converter using Xarray

This project demonstrates how to read multi-dimensional scientific datasets (e.g., NetCDF, GRIB, HDF, Zarr) using **Xarray** and convert them into a CSV file for easier analysis.

---

## 📌 Features
- Reads NetCDF (and similar formats) using `xarray`.
- Converts datasets into Pandas DataFrame format.
- Exports the data to a CSV file.

---

## 📂 Requirements
The following Python libraries are required:

- xarray
- netCDF4
- pandas
- xlsxwriter
- openpyxl

Install them with:
```bash
pip install xarray netCDF4 pandas xlsxwriter openpyxl
