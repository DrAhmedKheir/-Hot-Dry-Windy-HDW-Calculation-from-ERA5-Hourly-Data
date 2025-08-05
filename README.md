## Hot-Dry-Windy (HDW) Calculation from ERA5 Hourly Data

This repository includes the workflow for calculating HDW hours from ERA5 reanalysis data.

We computed HDW hours using hourly ERA5 reanalysis data, downloaded as monthly NetCDF files stored in compressed `.zip` format. Field locations and years were defined in `Locations.csv`, which included latitude, longitude, and phenological dates (sowing, anthesis, maturity) expressed as day-of-year (DOY). These DOY values were converted to calendar dates, accounting for cross-year sowing in winter crops.

For each month in the phenological periods of interest (Sowing → Anthesis, Sowing → Maturity, Anthesis → Maturity), the corresponding zipped ERA5 file was unzipped and read with **xarray**. Hourly variables included:
- **2 m air temperature (`t2m`, K)** – converted to °C
- **2 m dewpoint temperature (`d2m`, K)** – converted to °C
- **10 m wind components (`u10`, `v10`, m/s)** – combined into wind speed (m/s)

Relative humidity (RH, %) was calculated from air and dewpoint temperatures using the Clausius–Clapeyron relation.

An hour was classified as a **HDW hour** if all three thresholds were met simultaneously:
1. Temperature ≥ **32°C**
2. Relative humidity ≤ **30%**
3. Wind speed ≥ **7 m/s**

The number of HDW hours was summed for each phenological stage and location. This process was repeated for all site-years in the dataset, producing a CSV output containing HDW counts for the three growth periods per location-year.
<img width="1024" height="1536" alt="FlowdiagramForcalculatingHDW" src="https://github.com/user-attachments/assets/e9d69eda-5a45-482a-b4d1-<img width="1024" height="1536" alt="FlowdiagramForcalculatingHDW" src="https://github.com/user-attachments/assets/c4ed4aae-72a0-455b-b2a1-bc997d2849cf" />
<img width="1024" height="1536" alt="FlowdiagramForcalculatingHDW" src="https://github.com/user-attachments/assets/1677c3fe-9e67-4516-aa0c-0ed246626e25" />
b51b450f7391" />
