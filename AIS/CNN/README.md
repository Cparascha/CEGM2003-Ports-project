##Land–Water Segmentation and Polygon Classification

This project processes satellite imagery to classify predefined polygons as either berthing spots or anchoring spots in a port area.

A land–water mask is first generated from a satellite GeoTIFF. Because no manual labels are available, an automatic method is used to create a pseudo land–water mask based on image intensity. Otsu thresholding separates darker and brighter pixels, and morphological operations are applied to clean noise and fill small gaps. This pseudo mask is then used to train a U-Net segmentation model.

A U-Net architecture is chosen because it performs pixel-level segmentation and preserves spatial detail, which is important for land–water boundaries. The model is trained on image tiles and converges quickly due to the simplicity of the pseudo labels. Training is therefore limited to five epochs to avoid overfitting to noise in the automatically generated labels. After training, the model is applied to the full image to produce a georeferenced land–water mask.

Polygons are extracted from an exported Leaflet or Folium HTML file and reprojected to match the raster coordinate system. For each polygon, a buffer ring is created around its boundary and compared with the land–water mask. Polygons that touch land in at least one direction are classified as berthing spots, while polygons that are completely surrounded by water are classified as anchoring spots.

The outputs include a land–water GeoTIFF, a classified GeoJSON file, and an interactive HTML map for visual inspection.
