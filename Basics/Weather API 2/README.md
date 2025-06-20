# Weather Lookup Workflow

This workflow allows users to request the current weather for a specific city (and optionally country) using OpenStreetMap's geocoding API and Open-Meteo's weather data API.

## Overview

The workflow contains the following steps:

1. **Form Submission**  
   A form allows users to input a city and optionally a country.

2. **Get Coordinates**  
   The OpenStreetMap Nominatim API is queried to retrieve geographic coordinates for the given city.  
   **Important:** The node is configured with `alwaysOutputData: true` so that it **does not break** the workflow even if no results are found.  
   This allows error handling via the following IF node.

3. **Check if Coordinates Were Found**  
   An IF node checks whether the response contains `lat` and `lon` values. If not, a error message is returned.

4. **Get Weather**  
   If coordinates exist, Open-Meteo's API is queried using latitude and longitude.

5. **Success or Error Message**  
   Depending on the outcome, either a weather message or a city-not-found message is generated.

## Important Notes

- **Multiple Results Warning**:  
  The OpenStreetMap API may return **multiple results** for the same city name (e.g., "Springfield", "Paris").  
  This means the downstream nodes (e.g., `Get Weather`, `Set Message`) may be executed **multiple times**, once per result.  
  If you're using **paid APIs**, this can lead to **unexpected usage/costs**.  
  Always be cautious and consider adding a **limit** or filtering logic.

- **Error Handling Design**:  
  This workflow is built to handle errors gracefully by using:
  - `alwaysOutputData` on the coordinate-fetching node
  - `IF` conditions to branch execution cleanly

## APIs Used

- [OpenStreetMap / Nominatim](https://nominatim.openstreetmap.org)
- [Open-Meteo](https://open-meteo.com)

## Customization Tips

- Limit the number of results from OpenStreetMap using a filter or `limit=1` in the query
- Extend with email, push, Slack, or Telegram notifications
