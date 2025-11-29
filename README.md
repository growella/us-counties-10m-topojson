# U.S. counties TopoJSON (with Connecticut planning regions)

This repository provides a U.S. county-level boundary file at 1:10m scale, suitable for mapping and data visualization.

The file is based on the us-atlas@3 counties-10m TopoJSON, with one important change:

- Connecticut's 8 legacy counties (09001–09015) are replaced by Connecticut's 9 planning regions, which are now used as county-equivalents in many federal datasets, including 2026 conforming loan limits.

Outside Connecticut, all counties are unchanged from us-atlas.

The project is maintained by Homebuyer.com.

## File

- `data/us-counties-hb-with-ct-planning-regions.json`  
  TopoJSON FeatureCollection of county-level geometries for the United States, with Connecticut planning regions in place of Connecticut counties.

Each feature includes:

- `GEOID`: 5-digit county FIPS code  
- `STATEFP`: 2-digit state FIPS code  
- `COUNTYFP`: 3-digit county (or county-equivalent) FIPS code  
- `NAME`: county or county-equivalent name  

In Connecticut, `GEOID` and `COUNTYFP` use planning region FIPS codes 09110–09190 instead of county codes 09001–09015.

## Connecticut planning regions change

In this file, the legacy Connecticut counties are removed:

- 09001 Fairfield County  
- 09003 Hartford County  
- 09005 Litchfield County  
- 09007 Middlesex County  
- 09009 New Haven County  
- 09011 New London County  
- 09013 Tolland County  
- 09015 Windham County  

They are replaced by the nine Connecticut planning regions as county-equivalents:

- 09110 Capitol Planning Region  
- 09120 Greater Bridgeport Planning Region  
- 09130 Lower Connecticut River Valley Planning Region  
- 09140 Naugatuck Valley Planning Region  
- 09150 Northeastern Connecticut Planning Region  
- 09160 Northwest Hills Planning Region  
- 09170 South Central Connecticut Planning Region  
- 09180 Southeastern Connecticut Planning Region  
- 09190 Western Connecticut Planning Region  

This matches how recent datasets (including 2026 conforming loan limits) key Connecticut to planning regions instead of counties.

## Using the file via CDN

Once this repo is public, you can load the TopoJSON using jsDelivr.

Example (replace `YOUR_GITHUB_USERNAME` and optionally pin to a tag or commit):

`https://cdn.jsdelivr.net/gh/growella/us-counties-10m-topojson@main/data/us-counties-hb-with-ct-planning-regions.jsonn`

Example usage with d3 and topojson-client:

```js
import { json } from "d3-fetch";
import { feature } from "topojson-client";

const url = "https://cdn.jsdelivr.net/gh/growella/us-counties-10m-topojson@main/data/us-counties-hb-with-ct-planning-regions.json";

async function loadCounties() {
  const topo = await json(url);
  const counties = feature(topo, topo.objects.counties);
  console.log(counties.features[0].properties);
}

loadCounties();
```

The TopoJSON object is expected to be named `counties`.

## Data sources

Base U.S. counties:

- us-atlas@3 `counties-10m.json`, derived from U.S. Census Bureau cartographic boundary shapefiles.  
- License: ISC.

Connecticut planning regions:

- Official Connecticut Planning Regions boundary layer from the State of Connecticut geodata portal and Office of Policy and Management.

This repository is not an official product of the U.S. Census Bureau, FHFA, or the State of Connecticut.

## About Homebuyer.com

[Homebuyer.com](https://homebuyer.com) builds tools and content to make mortgages and home buying easier to understand.

We use this counties file for visualizing conforming loan limits and mortgage data, and are publishing it so other developers and data teams do not have to rebuild the same Connecticut planning region merge.
