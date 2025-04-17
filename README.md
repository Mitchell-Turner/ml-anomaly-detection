Invoice Anomaly Detection
This Python script performs invoice anomaly detection using the Isolation Forest algorithm from the scikit-learn library. It loads invoice data from a CSV file, performs feature engineering, fits an Isolation Forest model, flags anomalies, computes per-feature z-scores for explanation, and exports the flagged anomalies along with their explanations to an Excel file.
Requirements

Python 3.x
scikit-learn
pandas
numpy
openpyxl

To install the required libraries, run:
pip install scikit-learn pandas numpy openpyxl
Usage
To run the script, use the following command:
python invoice_anomaly_detection.py --input_csv master_invoices.csv \
                                    --output_excel anomalies.xlsx \
                                    --contamination 0.002 \
                                    --features "AP Amount" "Supplier" "Invoice Date" \
                                    --z_threshold 3.0
Parameters

--input_csv (str): Path to the input CSV file containing invoice data. Default is 'master_invoices.csv'.
--output_excel (str): Path to the output Excel file for anomalies and explanations. Default is 'invoice_anomalies_with_reasons.xlsx'.
--contamination (float): Proportion of data points to be flagged as anomalies. Default is 0.002.
--features (list): List of feature column names to use for anomaly detection. Default is ['AP Amount', 'Supplier', 'Invoice Date'].
--z_threshold (float, optional): Threshold for filtering anomalies based on z-score. Default is None.

Functionality
The script performs the following steps:

Loads the master invoice CSV file.
Parses the 'Invoice Date' column if present in the specified features.
Performs feature engineering:

Creates a continuous month index (e.g., Jan 2022 → 1, Feb 2022 → 2, etc.).
Encodes the 'Supplier' column as a numeric vendor code.


Builds a feature matrix for the model.
Handles missing values by aligning the DataFrame with the feature matrix and dropping rows with NaNs.
Fits an Isolation Forest model using the specified contamination parameter.
Scores and flags anomalies based on the fitted model.
Computes per-feature z-scores for explanation.
Determines the top driver feature and its z-value for each flagged anomaly.
Filters the anomalies based on the specified z-score threshold (if provided).
Exports the flagged anomalies along with their explanations to an Excel file.
Logs the summary of the anomaly detection process.

Example Output
The script will generate an Excel file with the flagged anomalies and their explanations. It will also log the summary of the anomaly detection process, including the number of invoices scanned and anomalies flagged.
INFO:root:Loading input CSV: master_invoices.csv
INFO:root:Fitting Isolation Forest model
INFO:root:Applying z-score threshold: 3.0
INFO:root:Exporting anomalies to Excel: anomalies.xlsx
INFO:root:Scanned 5638 invoices, flagged 8 anomalies.
INFO:root:Anomalies with reasons written to: anomalies.xlsx
License
This project is licensed under the MIT License.
