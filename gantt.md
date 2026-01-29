## Project Timeline
**Phase 1 – Data Handling and Pre-processing (Weeks 2.4–2.5)**
- Literature review (AIS clustering, berth detection, validation methods)
- AIS data cleaning and preprocessing (signals below 1 knot, only cargos and tankers)
- Satellite data preprocessing (mosaic generation)
- Initial algorithm research and selection
- Preparation of mid-term presentation


**Phase 2 – Modeling and Analysis (Weeks 2.6–2.7)**
- Selection and justification of clustering methods
  - DBSCAN
  - k-means 
  - Spectral clustering 
- AIS clustering experiments
- Hyperparameter tuning and model selection
- Conversion of clusters to polygon representations


**Phase 3 – Validation and Evaluation (Weeks 2.8–2.9)**
- CNN formulation to classify land and water in order to split polygons into berthing and anchorage points
- Satellite-based labeling of port infrastructure
  - Manual annotation
  - Enhancing from shipnext
- Spatial alignment between AIS-derived polygons and satellite data
- Quantitative validation using spatial metrics:
  - Precision and Recall
- Comparative evaluation of clustering methods
- Sensitivity analysis and robustness checks


**Phase 4 – Results Interpretation and Visualization (Week 2.10)**
- Final visualization of results
  - Maps of AIS clusters and split polygons
  - Overlays with satellite imagery
- Interpretation of validation metrics
- Final algorithm selection and justification

