AIzaSyCGjIm3Sil1WxWqa7qv1tSGtPRTNeBPEu0

# Atlas Compare

Atlas Compare is a responsive map-comparison workspace built with Leaflet. Select different map sources for each panel, compare measurements, and load local KML or GeoJSON data without uploading files to a server.

## Features

- Independent provider and layer selectors for both panels.
- Esri Streets, Esri Topographic, Esri World Imagery, and OpenStreetMap basemaps.
- Google Maps Roadmap, Satellite, Hybrid, and Terrain options through the official Google Maps JavaScript API.
- Add custom XYZ tile maps by URL, with optional API-key placeholders and attribution.
- Synchronized pan and zoom, with a switch to explore maps independently.
- Mirrored measurement points, with an option to draw independent paths.
- Distance and area calculations with a live A − B difference.
- Live cursor latitude/longitude and a mirrored cursor crosshair.
- KML (`.kml`, `.xml`) and GeoJSON (`.geojson`, `.json`) import. Imported features appear on both maps.
- GeoJSON export for measurements; undo the last point with right-click.
- Place search, browser geolocation, responsive layout, and English/French/Spanish/Arabic UI.

## Run locally

This is a static front-end project. No package installation or build step is required.

```sh
python3 -m http.server 8000
```

Open [http://localhost:8000/](http://localhost:8000/). A local HTTP server (or HTTPS hosting) is recommended for geolocation and API-key referrer restrictions. The application requires an internet connection for Leaflet and map tiles.

## Configure Google Maps

Google Maps needs a Google Maps Platform key with the **Maps JavaScript API** enabled and billing configured. Restrict the key to your local/production website referrers and only the APIs you use.

Select **Configure Google API key** and enter your restricted key. The app saves it in this browser, so the setup also works on GitHub Pages and does not request a private `map-config.local.js` file.

Browser-based API keys are visible to visitors and are not secrets. Use referrer restrictions and API restrictions; never use an unrestricted key. Without a configured key, selecting a Google map opens the key setup form; the other map sources work without a Google key.

The Google basemaps are loaded through [Leaflet.GridLayer.GoogleMutant](https://www.npmjs.com/package/leaflet.gridlayer.googlemutant), which uses Google's Maps JavaScript API rather than scraping Google tile URLs. Google Maps Platform terms, pricing, and quotas apply.

## Add a custom tile map

Select **Add map by URL** and provide a name, an XYZ tile URL template, and the attribution required by the tile provider. The URL must use `{z}`, `{x}`, and `{y}`. It may also use `{s}` for subdomains (enter subdomains such as `a,b,c`, or leave the field blank to use `a,b,c`) and `{apiKey}` for an optional API key. The saved source becomes available in both map selectors and is stored in this browser.

Custom map URLs and API keys are stored client-side and are visible to anyone using the page; browser-based keys are not secrets. Use provider-restricted keys and a tile service whose terms permit your use. This supports XYZ tile endpoints, not provider-specific APIs such as WMS/WMTS or JavaScript SDKs.

## Use the app

1. Choose a basemap independently for Map A and Map B.
2. Search for a location, use **My location**, or pan to the area of interest.
3. Enable **Mirror points** to copy every clicked point to both maps, or disable it to measure separately.
4. Choose **Distance** or **Area**, then click the map to add measurement vertices. Right-click either map to undo the last vertex.
5. Import a KML or GeoJSON file to display its supported features on both maps. Imports are processed locally in your browser and are limited to 20 MB per file.
6. Export measurement geometry as GeoJSON or clear measurements/imported features with their respective controls.

Distance is the sum of straight geodesic segments between clicks; this is not a road-routing service. Area is an approximate spherical measurement and is not intended for surveying. Imported features are visual overlays and do not change the measurement totals.

## Map data and attribution

| Provider | Map content | Attribution |
| --- | --- | --- |
| Esri ArcGIS MapServer | Streets, Topographic, World Imagery | Esri and the source credits shown on the map |
| OpenStreetMap / openstreetmap.de | Community map tiles | © OpenStreetMap contributors |
| Google Maps Platform | Roadmap, Satellite, Hybrid, Terrain | Google Maps |
| OpenStreetMap Nominatim | Place search | © OpenStreetMap contributors |

Esri imagery coverage varies by location and zoom. At its maximum available resolution, Esri may return tiles marked as unavailable; choose another Esri layer or provider for that area.

Third-party tile and search services have their own terms and usage limits. Public endpoints are not guaranteed production infrastructure. For high-volume or commercial use, use a provider plan appropriate to your deployment.

## Project files

- `index.html` — application structure and external library loading.
- `styles.css` — responsive visual design.
- `app.js` — maps, providers, measurements, imports, and interface behavior.

## License

No project license is currently specified. Map data and third-party libraries remain subject to their respective licenses and terms.
