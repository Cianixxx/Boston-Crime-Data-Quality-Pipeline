📌 Project Overview

This repository contains the code and documentation for the DaIQ-CRIMES-2025 project. The primary objective is to build a robust, well-documented, and fully reproducible Data & Information Quality pipeline. By analyzing the Boston Crime Incident Reports dataset (comprising crime.csv and offense_codes.csv), this project demonstrates how to effectively perform large-scale data cleaning to prepare complex datasets for downstream machine learning workflows.
🛠️ Technologies and Libraries

The pipeline is developed in Python and integrates a modern data science stack:

    Data Manipulation & Computation: pandas, numpy

    Automated Data Profiling: ydata-profiling, sweetviz

    Exploratory Visualization: matplotlib, seaborn, plotly

    Record Linkage & String Similarity: rapidfuzz, recordlinkage

    Preprocessing, Imputation, & Modeling: scikit-learn

⚙️ Pipeline Architecture

To guarantee maximum transparency and traceability, the workflow is strictly divided into three sequential phases. It adopts a hybrid approach, leveraging both domain-specific rule-based logic and advanced machine learning techniques.
1. Data Profiling and Quality Assessment

Before any transformations, the dataset undergoes rigorous profiling to establish a baseline.

    Automated & Manual Inspection: We analyze structural properties, missing value concentrations, and cross-field consistency (temporal, spatial, and categorical).

    Quality Dimensions: The data is evaluated across completeness, accuracy, consistency, uniqueness, validity, and plausibility using both custom rules and automated tools like ydata-profiling.

2. Data Cleaning and Standardization

This phase handles the systematic issues identified during profiling, preserving the original semantics of the data.

    Missing Values: We apply a multi-faceted imputation strategy. MICE (Multiple Imputation by Chained Equations) is utilized to capture multivariate dependencies for numerical and spatial attributes, while a KNN-based algorithm handles categorical features. Domain-specific logic is applied where appropriate (e.g., treating missing "SHOOTING" values explicitly as non-shooting incidents).

    Two-Stage Deduplication:

        Deterministic: Removal of exact duplicate rows.

        Probabilistic Record Linkage: A supervised Logistic Regression model classifies non-exact duplicate pairs based on temporal, spatial, and administrative similarities. Highly similar records are clustered using a graph-based approach to resolve duplicates under uncertainty without losing valid information.

    Text & Spatial Normalization: Resolving semantic inconsistencies using fuzzy string matching and standardizing location constraints.

3. Downstream Analysis & Validation

To quantitatively prove the impact of the data quality pipeline, a controlled downstream analysis is performed on both the "dirty" (original) and "cleaned" datasets.

    Task: A supervised classification model (Logistic Regression with class balancing) is trained to predict discrete crime categories.

    Results: The cleaned dataset successfully isolates the signal from the noise, demonstrating a consistent and systematic absolute improvement of +0.0052 in the macro F1-score compared to the uncleaned baseline.

👥 Authors

Developed as a group project in the Master's program in Computer Science at Politecnico di Milano:

    Daniele Spini 

    Oksana Batonova 

    Seyed Ali Chavoshian 
