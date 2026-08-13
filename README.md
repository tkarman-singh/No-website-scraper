# Local Business Finder — No Website Edition

A free Python tool that finds businesses near a specified location and identifies businesses that **do not have a website or social media presence listed on OpenStreetMap**.

> **100% free — no API keys, no billing, and no credit card required.**

The project uses free public services:

- **Nominatim** — converts an address or location into latitude/longitude coordinates.
- **Overpass API** — retrieves nearby business and place data from OpenStreetMap.
- **Pandas** — cleans and processes the retrieved data.
- **Folium** — displays the results on an interactive map.

---

## Features

- Search businesses within a configurable radius.
- Search using an address, city, landmark, or direct coordinates.
- Retrieve multiple types of businesses such as:
  - Restaurants
  - Cafés
  - Fast food
  - Banks
  - Pharmacies
  - Clinics
  - Dentists
  - Doctors
  - Veterinary services
  - Fuel stations
  - Car repair
  - Gyms
  - Cinemas
  - Theatres
  - Driving schools
  - Shops
  - Offices
  - Crafts
- Detect whether a business has a website or social-media presence listed in OpenStreetMap.
- Export businesses without web presence to a CSV file.
- Display identified businesses on an interactive map.
- Automatically fall back between multiple Overpass API mirrors if one is unavailable.

---

## How It Works

The notebook follows this workflow:

```text
Location / Address
       │
       ▼
   Nominatim
       │
       ▼
Latitude + Longitude
       │
       ▼
    Overpass API
       │
       ▼
OpenStreetMap Businesses
       │
       ▼
Clean & Process Data
       │
       ▼
Check Website / Social Presence
       │
       ├───────────────┐
       ▼               ▼
Has Web Presence   No Web Presence
                       │
                       ▼
                businesses_no_website.csv
                       │
                       ▼
                 Interactive Map