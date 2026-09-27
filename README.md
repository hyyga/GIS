# GIS
# GIS Flood Raster Analysis

## Overview

**GIS Flood Raster Analysis** is a Geographic Information System (GIS) project developed to analyze and visualize flood risk areas in **DKI Jakarta** using raster-based spatial analysis.

The project combines several spatial factors that influence flood susceptibility, including **elevation, rainfall, and proximity to rivers**. These factors are processed, standardized, aligned into a common spatial reference, and combined using a **Weighted Overlay** approach to produce a Flood Risk Index.

The final result is a spatial risk map that classifies areas in Jakarta based on their relative level of flood susceptibility.

---

## Objectives

The main objectives of this project are:

* Identify areas with relatively higher flood susceptibility in DKI Jakarta.
* Analyze the relationship between flood risk and key geographical factors.
* Integrate multiple raster datasets into a single flood risk index.
* Visualize the resulting flood-risk distribution using GIS.
* Demonstrate the application of raster-based spatial analysis for environmental risk assessment.

---

## Study Area

**Location:** DKI Jakarta, Indonesia

The analysis focuses on the Jakarta administrative area and its surrounding spatial characteristics, particularly elevation, rainfall distribution, and proximity to river networks.

---

## Data

The analysis uses several spatial datasets as input:

| Dataset             | Description                                            | Processing                                              |
| ------------------- | ------------------------------------------------------ | ------------------------------------------------------- |
| SRTM DEM            | Digital Elevation Model representing terrain elevation | Reclassified based on elevation threshold               |
| CHIRPS Rainfall     | Rainfall data for Jakarta                              | Processed and reclassified based on rainfall conditions |
| River Network       | River/drainage network                                 | Used to identify areas close to rivers                  |
| Building Footprints | Spatial representation of buildings                    | Rasterized and used as an optional supporting layer     |

### Main Raster Layers

The final analysis uses three primary raster factors:

* `near_river_aligned.tif`
* `low_elevation_aligned.tif`
* `jakarta_chirps_aligned.tif`

All relevant raster layers are aligned to a common spatial configuration before the weighted overlay process.

---

## Methodology

The overall workflow consists of several spatial-processing stages.

### 1. Data Preparation

Raw spatial datasets are collected and prepared for analysis. The datasets are clipped to the study area and converted into compatible spatial formats when necessary.

### 2. Rasterization and Reclassification

Vector-based spatial information, such as river proximity and building footprints, is converted into raster format.

The elevation and rainfall datasets are also reclassified into values representing their contribution to flood susceptibility.

For example:

* Lower elevation → higher flood susceptibility
* Higher rainfall → higher flood susceptibility
* Areas closer to rivers → higher flood susceptibility

### 3. Raster Alignment

All raster layers are standardized to ensure that they have compatible:

* Coordinate Reference System (CRS)
* Pixel size
* Spatial extent
* Raster alignment

The main processing configuration uses:

**CRS:** EPSG:32748
**Resolution:** 10 m

This step is important because raster calculations require corresponding cells from each input layer to represent the same geographic location.

### 4. Weighted Overlay

The standardized raster layers are combined using a weighted overlay approach.

The final model uses the following weights:

| Factor             | Weight |
| ------------------ | -----: |
| Proximity to River |   0.40 |
| Low Elevation      |   0.30 |
| Rainfall           |   0.30 |

The Flood Risk Index can therefore be represented as:

```text
Flood Risk Index =
(0.40 × River Proximity) +
(0.30 × Low Elevation) +
(0.30 × Rainfall)
```

A higher resulting value represents a greater combination of flood-related conditions.

### 5. Risk Classification

The resulting raster is reclassified into several flood-risk categories:

* **Very Low Risk**
* **Low Risk**
* **Medium Risk**
* **High Risk**

The classification is then visualized using a graduated raster symbology to make spatial patterns easier to interpret.

---

## Workflow

```text
Raw Spatial Data
       │
       ▼
Data Preprocessing
       │
       ├── DEM / Elevation
       ├── Rainfall
       └── River Network
       │
       ▼
Rasterization & Reclassification
       │
       ▼
Raster Alignment
       │
       ├── Common CRS
       ├── Common Resolution
       └── Common Extent
       │
       ▼
Weighted Overlay
       │
       ├── River Proximity      × 0.40
       ├── Low Elevation        × 0.30
       └── Rainfall             × 0.30
       │
       ▼
Flood Risk Index
       │
       ▼
Risk Classification
       │
       ▼
Flood Risk Map
```

---

## Output

The primary output of the analysis is:

```text
flood_risk_index.tif
```

This raster represents the calculated Flood Risk Index across the study area.

The resulting map can be used to visualize spatial patterns of flood susceptibility and identify areas where multiple flood-related factors overlap.

The GIS visualization is displayed over a basemap to provide geographical context and make the resulting risk distribution easier to interpret.

---

## Tools & Technologies

* **QGIS** — GIS processing and spatial analysis
* **Raster Calculator** — Weighted raster calculation
* **SRTM DEM** — Elevation data
* **CHIRPS** — Rainfall data
* **OpenStreetMap** — Basemap/reference visualization
* **GeoTIFF** — Raster data format

---

## Key Analysis

The project demonstrates how multiple environmental variables can be integrated into a single spatial model.

Areas with a combination of:

* relatively low elevation,
* higher rainfall conditions, and
* closer proximity to rivers

receive higher flood-risk values in the weighted overlay model.

The resulting spatial distribution can then be used as a basis for further GIS analysis, such as examining affected buildings, infrastructure, population exposure, or potential mitigation areas.

---

## Project Structure

```text
GIS-Flood-Raster-Analysis/
│
├── data/
│   ├── raw/
│   └── processed/
│
├── outputs/
│   ├── flood_risk_index.tif
│   └── flood_risk_map.png
│
├── qgis/
│   └── flood_risk_analysis.qgz
│
├── documentation/
│   └── workflow.png
│
└── README.md
```

> Large raster datasets are not necessarily included in this repository due to their file size. The repository can contain the processing workflow, project files, documentation, and final visualization.

---

## Limitations

This project uses a weighted overlay model, so the resulting flood-risk map represents a **relative spatial risk assessment**, rather than a direct prediction of actual flood depth or inundation extent.

The selected weights also represent the assumptions of the analysis. Different weights, thresholds, datasets, or classification methods may produce different results.

Therefore, the output should be interpreted as a GIS-based risk assessment and not as an official flood warning or disaster-management map.

---

## Future Development

Potential extensions of the project include:

* Incorporating historical flood events for validation.
* Adding land-use and land-cover information.
* Integrating population density and building exposure.
* Incorporating drainage and flood infrastructure data.
* Comparing the model with observed flood locations.
* Developing an interactive web-based flood-risk visualization.

