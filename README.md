# london-fire-station-information

This repo is to extract the locations of fire stations in London.

The station names are extracted from the [London Fire Brigade website](https://www.london-fire.gov.uk/community/your-borough/). Then the geocodes of the stations are obtained by using the [geopy library](https://geopy.readthedocs.io/en/stable/).

The locations can be manually checked on [Nominatim](https://nominatim.openstreetmap.org/).

The extracted data is stored in the `LFB_station_information.csv` file, which contains the station names and their corresponding geocodes (latitude and longitude) in the WGS84 coordinate system (EPSG:4326) and the British National Grid (EPSG:27700).

## Methods

1. **Web Scraping**: The station names are scraped from the London Fire Brigade website using Python's `requests` and `BeautifulSoup` libraries. This is done in `main.ipynb`.
2. **Geocoding**: The geocodes for each station are obtained using the `geopy` library, which interfaces with various geocoding services to convert station names into latitude and longitude coordinates. This is done in `main.ipynb`.
3. **Manual Checking**: The geocodes are manually checked. The postcodes of Lee Green and Plumstead are corrected, and the geocodes of Eltham and Hammersmith are removed due to the ambiguity of their station names ('Fire Station included'). The coordinates of these stations were removed. The results are stored in `Data/output_checked.csv`.
4. **Second Geocoding**: The geocodes of all stations with missing geocodes are obtained again by using the corrected station names. Then the locations are converted to the British National Grid (EPSG:27700). This is done in `check.ipynb`. The results are stored in `LFB_station_information.csv`, which is the same as `Data/output_final.csv`.
