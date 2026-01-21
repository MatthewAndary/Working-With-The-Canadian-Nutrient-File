# Food Segmentation Using the Canadian Nutrient File (CNF)
Viewable PDF found [here](https://github.com/MatthewAndary/Working-With-The-Canadian-Nutrient-File/blob/main/Working-Segmentation-Analysis.pdf)
## Overview
This project explores food segmentation using unsupervised learning, with a focus on macronutrient composition (protein, carbohydrates, and fat). Using data from Health Canada’s Canadian Nutrient File (CNF), foods are grouped based on nutritional similarity to understand patterns in dietary composition.

The initial objective was methodological:

> To get hands-on experience with clustering techniques (primarily K-means) and assess their usefulness for nutritional interpretation.

As the analysis progressed, important limitations of K-means emerged—especially around interpretability and stability—leading to a methodological pivot toward distribution-based ranking as a more transparent alternative.

## Data Source

Canadian Nutrient File (CNF)
Maintained by Health Canada, the CNF provides detailed nutrient composition data for thousands of foods.

Official documentation:
https://www.canada.ca/en/health-canada/services/food-nutrition/healthy-eating/nutrient-data.html

Data structure reference:
https://www.canada.ca/en/health-canada/services/food-nutrition/healthy-eating/nutrient-data/canadian-nutrient-file-compilation-canadian-food-composition-data-database-structure.html

## Methodology

1. Data Preparation & Cleaning

* Followed Health Canada’s CNF relational hierarchy
* Sequential merges: Food Groups → Food Names → Nutrients → Yield → Refuse → Conversion
* Removed French-language columns
* Pivoted nutrient data into a wide food × nutrient matrix

2. Nutrient Selection

Clustering was intentionally limited to three macronutrients: Protein, Total Fat, Total Carbohydrates (by difference)

Rationale:
* High completeness across foods (≥80%)
* Reduced dimensionality improves cluster geometry
* Focus on interpretability over predictive accuracy

## K-Means Clustering (Exploratory)

### Naïve Clustering

* Initial test with k = 3
* PCA used for visualization
* Demonstrated broad nutritional separation

### Choosing Optimal K

* Elbow Method (WSS)
* Silhouette Analysis
* Both methods suggested k ≈ 3–6 as plausible.

### Refined Clustering

* Final exploratory run with k = 6
* PCA visualization
* ANOVA tests confirmed statistically significant nutrient differences across clusters

### Visualization Highlights

* PCA scatter plots of clustered foods
* Elbow & silhouette plots for model selection
* Boxplots comparing nutrient distributions by cluster
* Violin plots showing overall macronutrient distributions
* Facet plots with embedded ANOVA statistics
* These visualizations helped diagnose both strengths and weaknesses of K-means for this problem.

## Interpretability Challenge

Despite statistically distinct clusters, meaningfully labeling clusters proved difficult:

* K-means centroids are non-parametric and seed-dependent
* Several clusters ranked similarly across multiple macronutrients
* Overlap (e.g., high-protein & high-fat foods) reduced uniqueness

## Resulting Decision

* K-means was abandoned for interpretive purposes

* This was a deliberate analytical choice rather than a failure—highlighting the difference between prediction-oriented and explanation-oriented methods.


## Limitations of K-Means (Observed)

* Sensitive to random seed
* Poor interpretability for explanation
* Centroids often misaligned with real distributions

## Tools & Libraries

R, tidyverse, ggplot2, dplyr, cluster, psych, MASS, PCA, ANOVA, K-means
