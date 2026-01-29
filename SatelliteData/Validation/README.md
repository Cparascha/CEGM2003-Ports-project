# AIS Cluster Validation Against SAM and ShipNext

This repository contains the validation workflow for comparing AIS cluster polygons against satellite derived ground truth datasets. This code focuses only on evaluating spatial agreement between AIS derived clusters and reference polygons from SAM and ShipNext.

AIS cluster outputs are provided as interactive HTML map. These files contain polygon geometries representing vessel activity regions. The validation compares these AIS polygons against two independent ground truth sources:

- SAM labeled polygons

- ShipNext polygons

Both ground truth datasets are provided as GeoPackage files.

## Validation Workflow
AIS polygons are first extracted directly from the HTML map files by parsing the embedded polygon coordinates. These polygons are converted into geospatial objects and reprojected together with the ground truth datasets into a common metric coordinate reference system to allow accurate area based comparisons.

Each AIS polygon is spatially compared against all ground truth polygons. For every AIS polygon, the ground truth polygon with the highest spatial overlap is selected as the best match. Spatial indexing is used to ensure the comparison is computationally efficient.

After the initial validation, the AIS polygons are exported to GeoPackage format. Anchorage areas are then manually removed using GIS software to isolate berth and terminal activity. The cleaned GeoPackages are validated again using the same methodology to quantify the impact of anchorage removal.

## Statistical Basis of the Comparison 
The core metric used for validation is Intersection over Union. Intersection over Union is defined as the area of overlap between an AIS polygon and a ground truth polygon divided by the total area covered by both polygons. Values range from zero to one, with higher values indicating better spatial agreement.

Validation is performed at multiple Intersection over Union thresholds. At each threshold, AIS polygons are classified as true positives or false positives based on whether they meet the overlap criterion. Ground truth polygons that are not matched by any AIS polygon are counted as false negatives.

From these classifications, standard detection metrics are computed:

- Precision measures how many AIS detections are correct

- Recall measures how many ground truth locations are detected

- F1 score provides a balanced summary of precision and recall
