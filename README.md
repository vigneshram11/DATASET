# DATASET
README – Synthetic Drug Consumption Dataset Preprocessing
1. Dataset Source
The dataset used in this project is the Synthetic Drug Consumption Dataset stored in CSV format.
Dataset file: synthetic_drug_consumption_raw.csv
The dataset was loaded into Google Colab from Google Drive using the Pandas library.

File path:
/content/drive/MyDrive/synthetic_drug_consumption_raw.csv
The dataset is synthetic and is used for demonstrating data preprocessing, cleaning, outlier handling, and visualization techniques.

2. Dataset Size Before Preprocessing

Before preprocessing, the dataset contained:
Number of rows: [5000]
Number of columns: [11]

These values were obtained using:

df.shape
or:
print(f"Initial Rows: {df.shape[0]}, Initial Columns: {df.shape[1]}")

3. Problems Identified
The following data-quality problems were identified during preprocessing:

Missing categorical/timing values

Categorical and timing columns were checked for missing values. Rows containing missing values in these columns were removed because incomplete categorical information could affect subsequent analysis.

Missing numerical values

Numerical columns were checked for missing values. Any remaining missing numerical values were handled using the median of the corresponding column.

Numerical outliers

Outliers were identified in numerical columns using the Interquartile Range (IQR) method.

The boundaries were calculated as:

Lower Bound=Q1−1.5(IQR)
Upper Bound=Q3+1.5(IQR)

Values outside these limits were treated as outliers.

4. Preprocessing Techniques Applied

The following preprocessing techniques were applied:

4.1 Loading the dataset

The CSV dataset was loaded using Pandas:

df = pd.read_csv(file_path)
4.2 Handling missing categorical/timing data

Non-numerical columns were identified using:

cat_cols = df.select_dtypes(exclude=[np.number]).columns

Rows containing missing values in these columns were removed using:

df.dropna(subset=cat_cols, inplace=True)
4.3 Outlier detection

The IQR method was used to identify outliers in numerical columns.

4.4 Outlier replacement

Detected outliers were temporarily converted to NaN and replaced using linear interpolation:

df[col] = df[col].interpolate(
    method='linear',
    limit_direction='both'
)

This preserves the row rather than deleting observations containing numerical outliers.

4.5 Filling remaining missing numerical values

Any remaining missing numerical values were replaced using the column median:

df[col] = df[col].fillna(df[col].median())
4.6 Data visualization

A histogram and boxplot were generated to examine the distribution of the numerical data and verify the effect of outlier treatment.

5. Dataset Size After Preprocessing

After preprocessing, the dataset contained:

Number of rows: [4707]
Number of columns: [11]

The number of columns normally remains unchanged because the preprocessing code does not delete any columns.

The number of rows may decrease because rows with missing categorical/timing values are removed.

6. Final Cleaned Dataset

The cleaned dataset was saved as:

synthetic_drug_consumption_cleaned.csv

Recommended output path:

/content/drive/MyDrive/synthetic_drug_consumption_cleaned.csv

The final dataset contains:

Cleaned categorical/timing information
Numerical missing values handled
Numerical outliers treated using the IQR method
Outliers replaced using linear interpolation
Remaining numerical missing values replaced with the median

The cleaned CSV file can be used for further data analysis, visualization, machine learning, and statistical modelling.
Raw dataset: synthetic_drug_consumption_raw.csv
Cleaned dataset: synthetic_drug_consumption_cleaned.csv
