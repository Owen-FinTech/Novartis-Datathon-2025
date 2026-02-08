# Novartis Datathon 2025

Forecasting pharmaceutical sales volume erosion following generic entry.

## Overview

When a drug patent expires and reaches its Loss of Exclusivity (LOE) date, generic manufacturers can enter the market with significantly lower development costs. This creates **generic erosion** - a decline in the original brand's sales volume. Accurately forecasting this erosion is critical for strategic planning and revenue forecasting in the pharmaceutical industry.

## Challenge Objectives

### Data Science Challenge

Forecast the volume of erosion following generic entry at two distinct time points:

1. **Scenario 1**: Right after generic entry (months 0-23)
2. **Scenario 2**: 6 months after generic entry (months 6-23)

### Business Challenge

- Conduct deep exploratory analysis of data preprocessing, with special focus on **high-erosion cases**
- Use visualization tools to make findings clear
- Provide explainable and simple results

## Generic Erosion Classification

Erosion is calculated over a **24-month horizon** and classified into three buckets:

- **Bucket 1 (B1)**: High Erosion (0-0.25) - *main focus of datathon*
- **Bucket 2 (B2)**: Medium Erosion (0.25-1)
- **Bucket 3 (B3)**: Low Erosion (>1)

## Data Provided

The challenge uses **2,293 country-brand combinations** that experienced generic entry:

### Training Set (1,953 observations)

- Up to 24 months of volume **before** generic entry
- Up to 24 months of volume **after** generic entry

### Test Set (340 observations)

- **Scenario 1** (~2/3 of test set; 228 observations): forecast months 0-23
- **Scenario 2** (~1/3 of test set; 112 observations): forecast months 6-23
- High Erosion (B1) represents approximately 20% of the test set for both scenarios

### Data Files

1. **df_volume.csv**: Volume of sales before and after generic entry
   - `months_postgx`: 0 = generic entry date, negative values = months before entry
   - `volume`: Number of drugs sold (target variable)

2. **df_generics.csv**: Information about generic competition
   - `n_gxs`: Number of generics (may vary over time)

3. **df_medicine_info.csv**: Drug and administration information by country
   - `hospital_rate`: Percentage of drug delivered in hospitals
   - `biological`: Whether drug is derived from a living organism
   - `small_molecule`: Whether drug is a low molecular weight compound (typically synthesized chemically)

### Note on Data Files in Repository

**Data Privacy Compliance**: In accordance with the datathon organizers' requirements, all CSV files in this repository contain only column headers with no actual data rows. This preserves the data structure and allows the code to be shared publicly while protecting the proprietary datasets provided by Novartis. The original datasets remain confidential and are not included in version control.

## Evaluation Metrics

All metrics are **normalized by the average monthly volume of the last 12 months before generic entry** to account for brand magnitude.

### Phase 1a: Scenario 1 Evaluation

- Absolute monthly error of all 24 months (20%)
- Absolute accumulated error of months 0-5 (50%)
- Absolute accumulated error of months 6-11 (20%)
- Absolute accumulated error of months 12-23 (10%)

**Top 10 teams** advance to Phase 1b.

### Phase 1b: Scenario 2 Evaluation

- Absolute monthly error of months 6-23 (20%)
- Absolute accumulated error of months 6-11 (50%)
- Absolute accumulated error of months 12-23 (30%)

**Top 5 teams** advance to final jury evaluation.

### Final Prediction Error (PE)

The weighted sum of averages across the 2 buckets, where **Bucket 1 (high erosion) is weighted twice as much as Bucket 2**.

## Winner Selection Process

1. **Phase 1**: Model Evaluation
   - Teams submit volume predictions for entire test dataset
   - Top 10 teams evaluated on Scenario 1 accuracy
   - Top 5 teams evaluated on Scenario 2 accuracy

2. **Phase 2**: Jury Evaluation
   - Teams present methodology, insights, and conclusions
   - Jury selects top 3 winning teams

## Key Notes

- Volume may be reported in different units (milligrams, packs, pills, etc.) depending on country-brand combination
- Categorical variables can be assumed to remain constant over time
- All provided data may be used for model training
- Explainability and simplicity of results will be valued
- Bucket information is not included in the dataset but can be derived
