In this section, three unsupervised clustering techniques are being performed (shown and elaborated in the three folders). 

### K-Means
K-Means partitions the data into a fixed number of clusters by minimizing within-cluster variance.  
Each cluster is represented by a centroid, and every data point is assigned to the nearest centroid.

- Assumes compact, roughly spherical clusters
- Automatically specifying the number of clusters (using Elbow plot)
- Computationally efficient but sensitive to initialization and outliers

### DBSCAN
DBSCAN (Density-Based Spatial Clustering of Applications with Noise) groups points based on local density rather than distance to a centroid.

- Clusters are defined as dense regions separated by low-density gaps
- Automatically identifies noise and outliers
- Automatically specifying the number of clusters (using Elbow plot)


### Spectral Clustering
Spectral clustering models the data as a similarity graph and identifies clusters by partitioning this graph along weak connections.

- Automatically specifying the number of clusters
- Computationally expensive for large datasets (this is the case here) 



The folder named "CNN" contains a U-Net that identifies land and water and then by giving an html of polygons for the above mentionded algorithms, it classifies trhe polygons in berthing and anchoring spots based on the surrounding pixels. If the surrounding pixels are only water , the polygon is classified as anchoring spot. If the surrounding pixels contain land, the polygon is classified as berthing spot. In order for teh CNN to run, the tiff file needs to be downloaded throught this link: https://surfdrive.surf.nl/s/2weXoi8gFA5358A 
