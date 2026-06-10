# London Fire Station Information

This repo is to extract the locations of fire stations in London.

The station names are extracted from the [London Fire Brigade website](https://www.london-fire.gov.uk/community/your-borough/). Then the geocodes of the stations are obtained by using the [geopy library](https://geopy.readthedocs.io/en/stable/).

The final data is stored in the `LFB_station_information.csv` file, which contains the station names, their corresponding geocodes (latitude and longitude) in the WGS84 coordinate system (EPSG:4326) and the British National Grid (EPSG:27700), and some additional information.

Note: Lambeth River Fire Station does not have mobilisation records in LFB mobilisation datasets.

## Station Opening and Closures

Harold Hill Fire Station is the only new station in LFB that has been opened since 2009. The official open date is 11 Feb 2010, but the fist mobilisation data of the station is on 29 Jan 2010.

The following stations have been closed. They are not included in the final output.

|Name           |Closing Date*|
|---------------|-------------|
|Belsize        |9 Jan 2014   |
|Bow            |9 Jan 2014   |
|Clerkenwell    |9 Jan 2014   |
|Downham        |9 Jan 2014   |
|Kingsland      |9 Jan 2014   |
|Knightsbridge  |9 Jan 2014   |
|Silvertown     |9 Jan 2014   |
|Southwark      |9 Jan 2014   |
|Westminster    |9 Jan 2014   |
|Woolwich       |9 Jan 2014   |
|Dartford       |29 Mar 2023  |
|Esher          |11 May 2025  |
|Buckinghamshire|18 Aug 2025  |
|Essex          |7 Nov 2025   |

* The closing date is based on the last apprearance of the mobilisation data of the station.

## Coordinate Processing Methods

1. **Web Scraping**: The station names are scraped from the London Fire Brigade website using Python's `requests` and `BeautifulSoup` libraries. This is done in `main.ipynb`.
2. **Geocoding**: The geocodes for each station are obtained using the `geopy` library, which interfaces with various geocoding services to convert station names into latitude and longitude coordinates. This is done in `main.ipynb`.
3. **Manual Checking**: The geocodes are manually checked. The postcodes of Lee Green and Plumstead are corrected, and the geocodes of Eltham and Hammersmith are removed due to the ambiguity of their station names ('Fire Station included'). The coordinates of these stations were removed. The results are stored in `Data/output_v1_checked.csv`.
4. **Second Geocoding**: The geocodes of all stations with missing geocodes are obtained again by using the corrected station names. Then the locations are converted to the British National Grid (EPSG:27700). This is done in `check.ipynb`. The results are stored in `LFB_station_information.csv`, which is the same as `Data/output_v2.csv`.
5. **Manual Checking**: The geocodes are manually checked again on Google Maps by entering the coordinates and comparing them with the actual locations. The geocodes of the following stations are corrected: Hainault, Chingford, Euston, Enfield, Hornsey, Heston, Bexley, Lee Green, Deptford, Forest Hill, New Cross. The results are stored in `Data/output_v2_checked.csv`. 
6. **Final Output**: The final output is stored in `Data/output_v3.csv` with additional information. The data processing steps are documented in `check2.ipynb`.

## Additional Information

1. Command: https://lfbenthusiast.wordpress.com/lfb-fire-stations/
2. Callsign: https://www.london-fire.gov.uk/media/4998/foia43101.pdf
