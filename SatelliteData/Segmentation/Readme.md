# Satellite Image Segmentation with Segment Anything (SAM)

This repository contains code to segment a **georeferenced satellite GeoTIFF** using Meta AI’s **Segment Anything Model (SAM)**.  
It supports a **CPU-only workflow** (reliable on machines without a working GPU) and produces:

- **Image tiles** (4×4 grid)
- **Colored overlay previews** of SAM segments per tile
- A **GeoPackage (.gpkg)** with all segment polygons in the **original CRS**

---

## What’s in this repo

- `merged_satellite.tif` —> input GeoTIFF *(placeholder in this repo; see SURF drive for the full file: https://surfdrive.surf.nl/s/2weXoi8gFA5358A?openfile=true)*
- `merged_satellite_try2.tif` — >input GeoTIFF - smaller version of merged_satellite to make computing times faster *(see SURF drive for the file:https://surfdrive.surf.nl/s/Hg66iPWKaSDjwCx?openfile=true)*
- `tiles_4x4_overlays/` —> overlays showing SAM segments per tile *(placeholder in this repo; see SURF drive for the full files: https://surfdrive.surf.nl/s/9xg8HqqH6EC2knm )*
- `port_la_segments.gpkg` —> polygonized SAM segments in the original CRS
- `SAM_labelled_polygons.gpkg` —> manually cleaned in QGIS version of `port_la_segments.gpkg` containing only the **berths and jetties**
- `Satellite_to_Segments.ipynb` —> first attempt at segmentation
- `Segmentation.ipynb` —> second attempt at segmentation *(cleaned code to remove errors)*

---

## Requirements

- Python 3.12.2+ recommended
- Key packages:
  - `rasterio`, `geopandas`, `shapely`, `affine`
  - `opencv-python`, `matplotlib`, `Pillow`, `numpy`
  - `segment-anything` (Meta SAM)

> Note: the script installs dependencies automatically via pip. In managed environments you may prefer to install them manually.

---

## How it works (pipeline summary)

1. **Load** the GeoTIFF with `rasterio` to get CRS + affine transform  
2. **Convert** the first 3 bands into an RGB image (with simple percentile stretch)
3. **Split** the raster into `GRID_N × GRID_N` tiles (default: 4×4)
4. Run **SAM automatic mask generation** on each tile
5. **Overlay** segments for visualization
6. **Polygonize** each mask and write all polygons to a **GeoPackage** with the original CRS

---

## Running the code

### 1) Place your input GeoTIFF
This code was run in a Runpod machine that we had access to upon request to Riccardo
Put your georeferenced GeoTIFF in the same directory as the script/notebook and set:

```python
IMAGE_PATH = "merged_satellite.tif"

```
If the merged_satellite.tif is too large use

```python
IMAGE_PATH = "merged_satellite_try2.tif"

