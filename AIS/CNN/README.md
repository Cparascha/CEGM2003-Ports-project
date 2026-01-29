### What this project does

This project takes a satellite GeoTIFF of a port area and produces a land and water map. It then uses that map to classify each polygon from an exported HTML file as either a berthing spot or an anchoring spot. A polygon is classified as berthing when it touches land in at least one direction, based on the pixels around it. It is classified as anchoring when it is surrounded by water. The final outputs are a GeoJSON file with the classification results and an interactive HTML map that lets you visually inspect the polygons and their labels.

### How the land and water mask is created

The first step is to create a land and water mask from the satellite image. Because no hand labeled ground truth is available, a simple automatic method is used to generate a first mask. The image is converted to a viewable format and an Otsu threshold is applied on valid pixels to separate dark and bright regions, which roughly correspond to water and land. Morphological operations are then applied to clean the result by removing small noise and filling small holes. This produces a pseudo label mask, which is then used as training target for the neural network.

### Why a U Net model was used

A U Net is well suited for this task because it performs pixel level segmentation. It predicts a class for every pixel rather than producing a single label for the whole image. It also works well when objects have clear boundaries, such as coastlines and land water transitions, and it can learn local spatial patterns from image tiles. The skip connections in U Net help preserve fine details while also using larger context, which is useful when boundaries are important.

### Why training was limited to 5 epochs

Training was run for 5 epochs because the model converged quickly and the training labels are pseudo labels generated from thresholding. In this setup, after a few epochs the model already learns to reproduce the pseudo mask well, and further training tends to bring diminishing returns. Training for longer can also lead the model to fit small artifacts in the pseudo labels, such as shadows or noise, rather than improving the real quality of the land water boundary. The final decision was supported by visually checking the produced land mask and the classification map.

### Outputs

The code produces two main outputs. The first is a GeoJSON file that contains all polygons and their classification, including useful debug fields such as whether land was detected around the polygon and how many pixels were evaluated. The second is an interactive HTML map that displays polygons in different colors for berthing and anchoring and provides tooltips for inspection.

### Notes

The required Python packages are listed in environment.yml. The code was developed and executed in VS Code, so file paths may need to be adjusted to match your local folder structure. If you run into issues, please contact one of the authors
