---
title: "Mapping Visibility: Applying Zone of Theoretical Visibility Analysis to the Gherkin"
date: 2026-04-12
categories:
  - GIS
  - Spatial Analysis
tags:
  - QGIS
  - viewshed
  - ZTV
  - remote sensing
  - renewable energy
  - spatial planning
header:
excerpt: "Exploring Zone of Theoretical Visibility analysis in QGIS — a technique widely used in renewable energy planning — and applying it to one of London's most recognisable landmarks."
---

While researching spatial planning methodologies used in the renewable energy sector, I came across Zone of Theoretical Visibility (ZTV) analysis — a technique I hadn't encountered in my coursework but which is fundamental to how wind farm applications are assessed in the UK planning system. Intrigued by the methodology, I decided to work through it myself before applying it to a more complex context.

## What is a ZTV?

A ZTV is a map showing all locations from which a structure could theoretically be seen, based purely on terrain and elevation data. The word "theoretical" is important — it assumes no vegetation, no intervening buildings, and a clear atmosphere. In practice it represents a worst-case visibility envelope, which is exactly what planning authorities need when assessing the visual impact of a proposed development.

In the context of wind farm planning, ZTVs are produced to identify sensitive receptors — residential properties, roads, National Scenic Areas, and heritage sites — that fall within the theoretical visibility zone of proposed turbines. Cumulative ZTVs layer multiple proposed or consented sites to assess combined visual impact, which is increasingly significant in Scotland where offshore and onshore wind development is dense.

## Why the Gherkin?

I chose 30 St Mary Axe — better known as the Gherkin — as my test case for a few reasons. Its height (179.8m to the apex) and distinctive profile make it easy to verify results intuitively. Central London's dense urban fabric also provides an interesting challenge: a standard bare-earth Digital Terrain Model would produce an unrealistically open viewshed, so I used a Digital Surface Model (DSM) incorporating building heights to ensure surrounding structures correctly occlude lines of sight.

## Methodology

The analysis was conducted in QGIS 3.44 using a 1m resolution LiDAR-derived DSM. Processing steps were as follows:

**Data preparation** — The DSM was clipped to a defined area of interest centred on the City of London. All layers were confirmed in EPSG:27700 (British National Grid) to ensure metric accuracy throughout. DSM resolution was adjusted to 5m.

**Observer point** — A grid polygon was created at the Gherkin's location. Because the DSM already encodes the building's height as an absolute elevation value (~195m ASL), the observer height was set to 0m — adding the building height on top would have double-counted the ground elevation and produced an inflated, inaccurate result. This is an important distinction when working with surface models rather than terrain models.

**Viewshed calculation** — The Viewshed tool was used with a target height of 1.6m (standing eye level) and an analysis radius of 20,000m. The binary output assigns a value of 1 to all cells with a theoretical line of sight to the observer point, and 0 to occluded areas.

## Result

{% include figure image_path="/assets/images/gherkin_ztv_result.jpg" alt="ZTV map showing theoretical visibility of the Gherkin across central London" caption="Zone of Theoretical Visibility for 30 St Mary Axe (the Gherkin), London. Red areas indicate theoretical visibility; grey areas are occluded by surrounding buildings or terrain." %}

The output illustrates how effectively London's existing building stock occludes visibility even for a structure of this height. The Thames corridor and open areas to the east show predictably higher visibility, while the dense building fabric immediately surrounding the City creates significant occlusion even at relatively short distances.

## Relevance to Offshore Wind Planning

This exercise maps directly onto how ZTV analysis functions in a marine spatial planning context — the focus of my dissertation on spatial use conflicts in the Moray Firth. Offshore turbines present a different challenge: the absence of intervening structures over open water means visibility ranges are far greater, and the relevant receptors extend to coastal communities, shipping lanes, and designated landscapes. Understanding the mechanics of ZTV production — particularly the DSM versus DTM distinction and the implications for observer height — is a prerequisite for interpreting or producing these outputs in a professional context.

The technique is also directly relevant to cumulative impact assessment, where the interaction between multiple wind farm ZTVs must be mapped and communicated clearly to planning authorities and the public. This is an area I'm keen to develop further.

## Reflections

Working through this from scratch surfaced a number of methodological decisions that are easy to overlook when using a tool procedurally: the choice of surface model, the handling of observer height, the appropriate analysis radius, and the implications of raster resolution on both accuracy and processing time. These decisions matter significantly when outputs may be tested at Public Inquiry — a standard requirement for major renewable energy applications in Scotland.

The analysis took approximately 35 minutes at 5m resolution over a 20km radius, highlighting the practical trade-off between resolution and processing efficiency that any GIS analyst working with large-area viewshed calculations will encounter.

---

*Tools used: QGIS 3.44, GDAL Viewshed, LiDAR DSM (1m resolution)*  
*All analysis conducted in EPSG:27700 (British National Grid)*
