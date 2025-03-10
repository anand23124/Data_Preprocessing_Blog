# Time-Series Data Preprocessing: Handling Missing Values

This repository contains a case study on preprocessing time-series data with a focus on handling missing values in utility meter readings. The project demonstrates various imputation techniques that maintain data integrity and preserve underlying trends for accurate forecasting.

## Project Overview

In many real-world scenarios, time-series data often has irregularities, missing values, and aggregated readings. This project tackles a common challenge: how to accurately distribute an aggregated sum across missing time intervals while preserving the overall trend of the data.

### Problem Statement

A utility company collected meter readings at irregular intervals. The dataset had missing values for several intermediate timestamps, but the final recorded reading was an aggregated sum of all missing readings in that period. This inconsistency made it difficult to:

1. Analyze consumption trends
2. Forecast future values accurately
3. Perform reliable anomaly detection

### Dataset

The dataset (`march_april_dataset.csv`) contains utility meter readings recorded at 15-minute intervals. It has the following structure:

- `Timestamp`: Date and time of the meter reading
- `Reading`: The consumption/usage value at that timestamp (contains missing values represented as NaN)

The data spans March and April, with approximately 5,856 rows.

## Implemented Approaches

This repository implements four different approaches to handle missing time-series data:

### 1. Prophet-Based Imputation with Mean Adjustment

Uses Facebook's Prophet library to leverage time-series forecasting capabilities for estimating missing values while preserving identified trends. The method:
- Estimates missing values based on temporal patterns
- Scales the imputed values to match the known aggregated sum
- Preserves the underlying trend in the data

### 2. Mean-Based Imputation

A simpler approach that:
- Computes the mean of available readings
- Replaces missing values with this computed mean
- Validates imputation by ensuring sum consistency

### 3. IQR-Based Outlier Handling and Imputation

This method focuses on handling potential outliers that may arise from imputation:
- Uses Interquartile Range (IQR) to detect extreme values
- Applies linear interpolation for initial imputation
- Replaces outliers with the median to maintain stability
- Scales imputed values to match the expected total

### 4. K-Nearest Neighbors (KNN) Imputation

A more sophisticated approach that:
- Uses similarity between timestamps to estimate missing values
- Finds the k most similar timestamps based on numerical distance metrics
- Computes weighted averages of the neighbors to replace missing values
- Scales results to match the known aggregate sum

## How to Use This Code

### Prerequisites

```
pandas
numpy
matplotlib
scikit-learn
fbprophet (optional, for Prophet-based imputation)
```

### Installation

1. Clone this repository:
```bash
git clone https://github.com/anand23124/Data_Preprocessing_Blog.git
cd Data_Preprocessing_Blog
```

2. Install required dependencies:
```bash
pip install -r requirements.txt
```

3. For Prophet-based imputation (optional):
```bash
pip install prophet
```

### Running the Code

1. Place your dataset in the repository directory or update the file path in the code
2. Run the preprocessing script inside the notebook

This will:
- Apply all four imputation methods
- Save the results to separate CSV files
- Generate comparison visualizations (if visualization code is uncommented)

## Results and Comparison

Each approach has its strengths and limitations:

- **Prophet-based imputation**: Best for preserving temporal trends and patterns but requires more computational resources
- **Mean-based imputation**: Simple and fast but doesn't account for trends
- **IQR-based imputation**: Good for handling potential outliers in the imputed values
- **KNN imputation**: Effective for capturing non-linear patterns and relationships between nearby timestamps

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
