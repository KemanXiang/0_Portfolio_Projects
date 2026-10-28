# Brain MRI Image Segmentation Using K-Means Clustering

**Intensity-Based Unsupervised Learning, Model Selection, and Cross-Image Transfer**

**Author:** Keman Xiang  
**Portfolio focus:** Data Analytics · Unsupervised Machine Learning · R  
**Environment:** R, RStudio, R Markdown  
**Source material:** MIT OpenCourseWare, *15.071 The Analytics Edge*, Unit 6 recitation

## Project Overview

This project studies how unsupervised K-Means clustering can represent grayscale brain MRI images with a small number of intensity categories. We first explore and validate two pixel matrices, fit K-Means to a reference image, examine the trade-off between cluster count and reconstruction quality, and then **transfer the five learned centroids without refitting** to a second image.

Our objective is to evaluate **intensity quantization, model selection, and cross-image distribution shift**, providing quantitative evidence that warrants further investigation of potential tumor-related abnormalitiesn. The labels `healthy.csv` and `tumor.csv` identify the supplied instructional images.

## Research Questions

1. How do image dimensions, grayscale distributions, and background prevalence affect intensity-based segmentation?
2. How does the choice of cluster count influence within-cluster variation, explained intensity variance, and model stability?
3. What changes when a fixed intensity codebook learned from one image is applied to a second image?
4. What conclusions are supported by numerical reconstruction diagnostics, and which require clinical ground truth?

## Data

Each CSV cell contains a grayscale pixel intensity between 0 (black) and 1 (white). The matrices are images, not datasets of independent patients.

|Image|Dimensions|Pixels|Mean intensity|SD|Exact-zero pixels|Distinct intensities|
|---|---|---:|---:|---:|---:|---:|
|Healthy reference|566 × 646|365,636|0.1302|0.1257|9.30%|206|
|Tumor-labeled transfer image|571 × 512|292,352|0.1595|0.1715|34.67%|254|

Both files contain no missing pixel values. The images have different dimensions, and their zero-intensity shares differ substantially. Therefore, we compare **within-image cluster percentages** rather than raw pixel counts alone, and we do not assume spatial registration or comparable acquisition conditions.

## Analytical Workflow

1. **Data exploration:** Import both CSV matrices, verify numeric ranges and completeness, reconstruct the images, and compare grayscale distributions.
2. **Reference segmentation:** Fit a five-cluster K-Means model on the healthy image (`set.seed(1)`, `iter.max = 1000`), inspect cluster centroids and pixel allocations, and reconstruct the segmented image.
3. **Model selection:** Examine `k = 2` through `10` using within-cluster sum of squares (WCSS), explained intensity variance, marginal gains, visual interpretability, and random-initialization sensitivity.
4. **Cross-image transfer:** Freeze the five healthy-image centroids, assign each second-image pixel to its nearest centroid, and compare cluster composition and grayscale reconstruction error.

The feature space contains **pixel intensity only**. Spatial coordinates, texture, neighborhood relationships, and anatomical labels are not inputs to K-Means.

## Key Results

### 1. Model selection: five clusters as an interpretable reference

|Clusters (k)|WCSS|Intensity variance explained|WCSS reduction vs. preceding k|
|---|---:|---:|---:|
|4|467.8845|91.8980%|44.5445%|
|5|302.1291|94.7683%|35.4266%|
|6|220.7184|96.1780%|26.9457%|

At `k = 5`, the reference model explains **94.7683% of the observed healthy-image intensity variation** in the in-sample K-Means decomposition. Increasing from four to five clusters reduces WCSS by **35.43%**, while increasing from five to six reduces it by another **26.95%**. We retain five clusters as a useful, interpretable reference—not as a uniquely proven optimum. Explained intensity variance is **not** clinical segmentation accuracy.

In ten single-start runs, the relative WCSS range was **0.62304% at k = 4** and **0.31117% at k = 5**. This indicates modest observed initialization sensitivity in the tested configuration, without establishing global optimality.

### 2. Cross-image transfer: fixed-centroid cluster composition

The following centroids were fitted **only on the healthy image** and then reused for the second image. Cluster IDs are ordered from darkest to brightest, rather than using arbitrary K-Means labels.

|Intensity cluster|Healthy centroid|Healthy pixels|Transfer pixels|Healthy share|Transfer share|Change (percentage points)|
|---|---:|---:|---:|---:|---:|---:|
|1 — darkest|0.02189|139,963|135,357|38.279%|46.299%|+8.020|
|2|0.11656|114,480|17,731|31.310%|6.065%|−25.245|
|3|0.20136|65,557|58,506|17.930%|20.012%|+2.083|
|4|0.32991|27,338|52,220|7.477%|17.862%|+10.385|
|5 — brightest|0.49139|18,298|28,538|5.004%|9.762%|+4.757|

The largest shift occurs in **cluster 2**, whose share falls by **25.245 percentage points**. Cluster 4 increases by **10.385 points**, while the darkest cluster increases by **8.020 points**. Because the centroids are held fixed, these are changes in the observed **grayscale-category distribution**, not artifacts of independently refitting two models. They do not identify a tumor region or anatomical tissue class.

### 3. Reconstruction error increases on the transfer image

|Image|MAE|MSE|RMSE|Total WCSS|
|---|---:|---:|---:|---:|
|Healthy (training)|0.022047|0.000826|0.028746|302.1291|
|Tumor-labeled (transfer)|0.029319|0.001573|0.039661|459.8580|

Under the fixed healthy-image codebook, the transfer-image **RMSE is approximately 38.0% higher** and **MAE approximately 33.0% higher**. These are grayscale reconstruction errors, not medical segmentation errors. Because the images contain different pixel counts, total WCSS is not directly size-normalized; MAE, MSE, and RMSE are more suitable cross-image comparisons.

|Image|Median absolute error|90th-percentile absolute error|Pixels outside centroid range|
|---|---:|---:|---:|
|Healthy|0.02085|0.04223|25.6356%|
|Tumor-labeled|0.02189|0.05540|46.4382%|

The higher 90th-percentile residual and greater proportion of pixels beyond the reference centroid range suggest that the transferred codebook represents the second image's intensity tails less closely.

### 4. Background sensitivity matters

|Image|Exact-zero share|Positive-intensity pixels|Positive-only mean|Positive-only median|
|---|---:|---:|---:|---:|
|Healthy|9.29504%|331,650|0.14358|0.11966|
|Tumor-labeled|34.66917%|190,996|0.24417|0.24314|

The transfer image has **25.374 percentage points more exact-zero pixels**. Excluding exact zeros also reveals a higher mean among its positive-intensity pixels. These differences indicate that both background prevalence and positive-intensity composition vary; neither difference can be attributed to pathology without matched acquisition conditions and ground-truth annotations. **Nonzero pixels are not a validated brain-tissue mask.**

## Interpretation and Limitations

The results demonstrate an intensity-based clustering workflow and a controlled test of **fixed-centroid transfer**. They provide evidence but do not verify tumor detection. In particular:

- Only two images are available; individual pixels are not independent patient observations.
- Grayscale intensity alone cannot establish anatomical identity or enforce spatial continuity.
- Different dimensions, backgrounds, acquisition settings, or preprocessing can produce apparent distribution shifts.
- No pixel-level ground-truth masks are supplied, so Dice, intersection-over-union, sensitivity, specificity, and diagnostic accuracy cannot be calculated.
- Five clusters provide a defensible working representation, but the elbow heuristic and initialization checks do not establish a unique global optimum.

For a data analytics portfolio, the methodological contribution is the discipline of **choosing segmentation granularity, preserving category definitions during transfer, measuring distribution changes, and distinguishing numerical fit from substantive validity**.

## Repository Structure

```text
Brain-MRI-Image-Segmentation/
├── README.md
├── data/
│   ├── healthy.csv
│   └── tumor.csv
├── analysis/
│   ├── 01_Data_Exploration.Rmd
│   ├── 02_KMeans_Segmentation.Rmd
│   ├── 03_Model_Selection.Rmd
│   └── 04_Cross_Image_Analysis.Rmd
 ── outputs/
    ├── html/
    └── Brain_MRI_Image_Segmentation_Portfolio_Research_Report.pdf

    
```

## Reproducibility

1. Install **R**, **RStudio**, and the packages required by the R Markdown documents, including `rmarkdown` and `knitr`.
2. Place the unmodified `healthy.csv` and `tumor.csv` files in `data/` (or in a directory supported by the documents' file-location helper).
3. Open each `.Rmd` in `analysis/` and knit to HTML in the order `01` → `02` → `03` → `04`.
4. Review the generated figures, numerical tables, and R session information. Keep the fixed-reference model and the separate model-selection / random-start experiments distinct when comparing WCSS values.

The source R Markdown files are the executable analyses; the portfolio report summarizes their executed results. This README reproduces the figures reported in that document and does not imply that a separate clinical validation was conducted.

## References

- MIT OpenCourseWare. [15.071 *The Analytics Edge* (Spring 2017)](https://ocw.mit.edu/courses/15-071-the-analytics-edge-spring-2017/), Unit 6 recitation.
- Google for Developers. [Evaluating K-Means Clustering Results](https://developers.google.com/machine-learning/clustering/kmeans/evaluate-results).
- Reinke, A. et al. [Towards a guideline for evaluation metrics in medical image segmentation](https://doi.org/10.1186/s13104-022-06096-y).
- Maier-Hein, L. et al. [Metrics reloaded: recommendations for image analysis validation](https://doi.org/10.1038/s41592-023-02151-z).

---

**Scope note:** This is a methodological analysis of supplied grayscale MRI matrices, **not** a clinically validated tumor-segmentation study.
