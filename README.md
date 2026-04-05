# Dugwell Detection from Satellite Imagery — Madhya Pradesh

> Deployed across all **55 districts** of Madhya Pradesh for the **MGNREGA Department**, Government of MP.

Automated dugwell detection system using YOLOv8 trained on high-resolution WorldView satellite imagery (0.3m). Built to support water conservation planning and rural infrastructure asset mapping across the entire state.

---

## Problem Statement

The MGNREGA department needed an accurate, state-wide inventory of dugwells (open wells) across Madhya Pradesh to support water conservation activities and resource planning. Manual identification from satellite imagery across 55 districts is impractical at scale — this project automates detection using deep learning.

---

## Solution Overview

```
WorldView Satellite Imagery (0.3m resolution, 2016)
                    │
                    ▼
        District-wise tile extraction
                    │
                    ▼
        512 × 512 patch generation
        (3,000 annotated patches)
                    │
                    ▼
        Annotation via Roboflow
        (bounding boxes, YOLOv8 format)
                    │
                    ▼
        Train/Val split — 80% / 20%
                    │
                    ▼
        YOLOv8 Training — 100 epochs
                    │
                    ▼
              F1 Score: 93%
                    │
                    ▼
        District-wise inference
        across all 55 MP districts
                    │
                    ▼
        Shapefile output per district
        (location + bounding box of each dugwell)
```

---

## Dataset

| Property | Details |
|----------|---------|
| Satellite | WorldView (DigitalGlobe) |
| Resolution | 0.3 m/pixel |
| Year | 2016 |
| Coverage | Selected districts across Madhya Pradesh |
| Patch size | 512 × 512 pixels |
| Total patches | 3,000 |
| Annotation tool | Roboflow |
| Format | YOLOv8 (YOLO txt format) |
| Train / Val split | 80% / 20% |

---

## Model Training

| Parameter | Value |
|-----------|-------|
| Model | YOLOv8 (Ultralytics) |
| Epochs | 100 |
| Input size | 512 × 512 |
| Task | Object Detection |
| F1 Score | **93%** |

- Annotations created using **Roboflow** with bounding boxes around each visible dugwell
- Dataset exported in YOLOv8-compatible format directly from Roboflow
- Model trained using Ultralytics YOLOv8 framework

---

## Inference — State-wide Deployment

After training, the model was applied **district by district** across all **55 districts of Madhya Pradesh**:

1. Load district boundary shapefile
2. Clip WorldView imagery to district extent
3. Generate 512 × 512 inference tiles
4. Run YOLOv8 detection on each tile
5. Convert detections to geographic coordinates (pixel → lat/lon)
6. Export as district-wise shapefiles for GIS use

---

## Output

- District-wise **shapefiles** with detected dugwell locations and bounding polygons
- Ready for import into QGIS / GeoServer
- Supports MGNREGA water conservation planning and asset verification

---

## Impact

| Metric | Value |
|--------|-------|
| Districts covered | 55 (all of Madhya Pradesh) |
| Detection F1 Score | 93% |
| Use case | Water conservation asset mapping |
| Department | MGNREGA, Government of MP |
| Deployed via | MPSEDC GIS infrastructure |

---

## Tech Stack

| Category | Tools |
|----------|-------|
| Model | YOLOv8 (Ultralytics) |
| Annotation | Roboflow |
| Satellite Data | WorldView 0.3m |
| Geospatial | GDAL, GeoPandas, Shapely, Rasterio |
| GIS Output | Shapefile, GeoJSON |
| Environment | Python, PyTorch, Linux |

> **Note:** Training data and model weights are maintained within MPSEDC's secure deployment environment (government project). This repository documents the methodology and pipeline.

---

## Author

**Nitesh Singh Bhadoriya**
AI & ML Engineer — MPSEDC, Bhopal
[LinkedIn](https://www.linkedin.com/in/nitesh-singh-bhadoriya-917411226) · [GitHub](https://github.com/nitesh-bhadoriya)

---

*Developed under the Madhya Pradesh State Electronics Development Corporation (MPSEDC) for the MGNREGA Department, Government of Madhya Pradesh.*
