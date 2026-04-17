---
title: "Portfolio"
permalink: /portfolio/
layout: single
author_profile: true
---

<details markdown="1">
<summary><strong>Moray Firth Offshore Wind — Spatial Conflict Analysis</strong></summary>

*University of St Andrews Dissertation, 2026–27*

A GIS-based Multi-Criteria Evaluation of spatial conflicts between proposed 
offshore wind development and existing maritime uses in the Moray Firth. 
The analysis integrates vessel traffic data, fishing activity, navigational 
routes, and environmental constraints to produce a weighted suitability surface 
identifying low-conflict development zones.

![Map of research area with offshore wind farms overlayed](/assets/images/moray_map.png)

**Methods:** MCE weighted overlay, DBSCAN clustering, kernel density estimation  
**Tools:** Python (geopandas, rasterio, scikit-learn, matplotlib), QGIS

*Interactive map and full write-up coming soon.*

</details>

---

<details markdown="1">
<summary><strong>East Anglia Onshore Wind Farm — Spatial Suitability Analysis</strong></summary>

*GG3209 Spatial Analysis with GIS, University of St Andrews, December 2025*

A GIS-based Multi-Criteria Evaluation identifying optimal sites for onshore 
wind farm development across a study area in coastal East Anglia. The region 
was selected for its proximity to existing offshore wind infrastructure and 
its position between London and Birmingham — two of the UK's highest energy 
demand centres.

**The analytical challenge** was that broad suitability across the study area 
was high. It was necessary to filter to locations exceeding 80% suitability 
before meaningful analysis between sites was possible. DBSCAN clustering 
was then applied to spatially group high-suitability pixels into discrete 
candidate zones, which were ranked by mean suitability score.

**MCE Factor Weightings**

| Factor | Weight | Rationale |
|---|---|---|
| Slope | 0.35 | Steep terrain significantly increases construction cost and turbine performance loss |
| Power proximity | 0.30 | Grid connection is the dominant infrastructure cost for onshore wind |
| River proximity | 0.15 | Flood risk and ecological constraints increase with proximity |
| Wind speed | 0.10 | Spatial variation across the AOI was limited, reducing discriminatory power |
| Road proximity | 0.10 | Access required but less cost-determining than grid connection |

Areas of Outstanding Natural Beauty were treated as a **hard boolean constraint** 
rather than a weighted factor — excluded entirely regardless of suitability score.

**Key finding:** The study area supports both large-scale centralised development 
and a distributed cluster approach. A distributed model offers grid resilience 
benefits and reduced transmission losses, while a single large site benefits 
from economies of scale in construction and maintenance. The analysis identifies 
candidate zones for both strategies.

**Methods:** MCE weighted overlay, boolean constraint masking, DBSCAN clustering, 
kernel density estimation  
**Tools:** Python (geopandas, rasterio, scikit-learn, matplotlib), QGIS

![MCE Suitability Map with Cluster Boundaries](/assets/images/imposed_mce.png)

<iframe 
  src="/assets/maps/norfolk.clusters.interactive.html" 
  width="100%" 
  height="500px"
  frameborder="0"
  onload="this.contentWindow.dispatchEvent(new Event('resize'))">
</iframe>

[View Code on GitHub](https://github.com/sambowyergis/Norfolk-Windfarm-MCE){: .btn .btn--primary target="_blank"}

</details>

---
