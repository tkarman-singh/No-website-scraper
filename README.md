# Local Business Finder — No Website Edition

A free Python notebook that finds named businesses near a location using OpenStreetMap and identifies businesses that **do not have a website or social-media presence listed in OpenStreetMap**.

> **Important:** A missing website tag in OpenStreetMap does **not** prove that a business has no website. Use the results as a lead list and verify businesses manually.

## Features

- 📍 Search by address, city, landmark, or direct coordinates
- 📏 Configurable search radius in kilometers
- 🏪 Searches shops, offices, crafts, and selected amenity types
- 🌐 Checks for website and selected social-media tags
- 📊 Produces a clean Pandas DataFrame
- 💾 Exports businesses without web presence to CSV
- 🗺️ Displays results on an interactive Folium map
- 🔑 Uses free, keyless public services — no API key or credit card required
- 🔄 Uses multiple Overpass API mirrors as fallbacks

## How It Works

```text
Address / Coordinates
        ↓
     Nominatim
   (Geocoding)
        ↓
  Latitude / Longitude
        ↓
     Overpass API
        ↓
 OpenStreetMap Businesses
        ↓
 Clean + Deduplicate Results
        ↓
Check website / social tags
        ↓
Businesses with no web presence listed
        ↓
       CSV + Map
```

### Data sources

- **Nominatim** — converts an address into latitude/longitude.
- **OpenStreetMap** — provides business/place data.
- **Overpass API** — queries OpenStreetMap features within the requested radius.

## Requirements

- Python 3.10+ recommended
- Jupyter Notebook / JupyterLab
- Internet connection

The notebook installs these packages:

```bash
pip install requests pandas folium
```

## Usage

1. Open `local_business_finder_no_website.ipynb` in Jupyter Notebook, JupyterLab, or VS Code.
2. Run the package-installation cell.
3. In **Step 1**, configure the search:

```python
ADDRESS = "Jagraon, Punjab, India"
RADIUS_KM = 5

LATITUDE = None
LONGITUDE = None
```

You can either provide an address or skip geocoding by supplying coordinates:

```python
LATITUDE = 30.79
LONGITUDE = 75.47
```

4. Modify `AMENITY_TYPES` if you want to include different types of businesses.
5. Run the remaining cells.
6. The notebook will generate:

```text
businesses_no_website.csv
```

7. The final cell creates an interactive map showing the search center and businesses without web presence listed in OpenStreetMap.

## Business Types

The notebook explicitly searches for these amenity types:

- Restaurant
- Cafe
- Fast food
- Bar
- Pub
- Bank
- Pharmacy
- Clinic
- Dentist
- Doctors
- Veterinary
- Fuel
- Car repair
- Cinema
- Theatre
- Driving school
- Gym
- Bureau de change
- Money transfer
- Studio

It also retrieves features tagged with `shop`, `office`, and `craft`.

## Output

The CSV contains businesses that have no website or selected social-media presence recorded in OpenStreetMap.

Typical columns include:

| Column | Description |
|---|---|
| `name` | Business name |
| `category` | OSM category such as `shop=...` or `amenity=...` |
| `address` | Address information available in OSM |
| `phone` | Phone number when available |
| `lat` | Latitude |
| `lon` | Longitude |

The notebook checks these tags when determining web presence:

```text
website
contact:website
facebook
contact:facebook
contact:instagram
```

## Project Structure

```text
.
├── local_business_finder_no_website.ipynb
├── businesses_no_website.csv      # generated after running the notebook
└── README.md
```

## Limitations

### OpenStreetMap completeness

OpenStreetMap is community-maintained. Business information can be incomplete, outdated, or missing.

Therefore:

```text
No website listed on OSM
        ≠
Business definitely has no website
```

The output should be treated as a **prospecting/lead-generation list**, not a verified database of businesses without websites.

### Search coverage

The notebook only searches the OSM categories and amenity types configured in `AMENITY_TYPES`, plus `shop`, `office`, and `craft` features. Businesses that are not mapped or appropriately tagged in OSM may not appear.

### Public API limits

The project uses free public Nominatim and Overpass services. Avoid running large-radius searches repeatedly or sending many requests in rapid succession.

The notebook includes multiple Overpass mirrors and falls back to another endpoint when one fails.

## Responsible Use

If you use the generated list for commercial outreach such as calls, SMS, or email campaigns, verify the businesses first and follow applicable rules regarding unsolicited commercial communication.

## License

This repository contains a notebook that uses publicly available OpenStreetMap services. Check the applicable OpenStreetMap/Nominatim and Overpass usage policies before deploying the project at scale.
