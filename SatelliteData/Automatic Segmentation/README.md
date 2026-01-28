## Note on SAM3 attempt (and why we use the `segmentation/` outputs)

An early goal of this project was to use **SAM3** to *automatically* identify and extract port features such as **berths** and **jetties** directly from the satellite imagery. This required additional setup (including **Hugging Face access tokens** and SAM3-specific loading/procedures). In practice, the SAM3 workflow did **not** perform as intended for our use case: the automatic segmentation tended to return **very large, coarse masks** (covering broad regions) rather than clean, feature-level segments for berths and jetties.

Because of this, we ultimately relied on the more stable and reproducible outputs contained in the **`segmentation/`** folder for the project deliverables. These outputs include the exported polygon layers and the cleaned subset focusing specifically on berths and jetties.
