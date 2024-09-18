
# Data Cleaning and Analysis for MATIC Transactions

This project performs data cleaning and analysis on a dataset related to Polygon/MATIC cryptocurrency transactions. The focus is on handling missing values, cleaning column names, and calculating historical prices for MATIC based on the dataset.

## Project Overview

The main objectives of this project are:
- Clean up the dataset by fixing column names and handling missing data.
- Perform analysis on historical MATIC prices and transaction values.
- Generate visualizations to help understand the trends and patterns in the data.

## Dataset

The dataset used in this project is named `polygon.csv`. It contains various transaction-related fields, including:
- `Blockno`: The block number of the transaction.
- `UnixTimestamp`: Timestamp of the transaction.
- `DateTime (UTC)`: Date and time of the transaction in UTC.
- `Value IN(MATIC)`: Value coming into the transaction.
- `Value OUT(MATIC)`: Value going out of the transaction.
- `CurrentValue @ $Price/MATIC`: Current value of MATIC.
- `TxnFee(MATIC)`: Transaction fee in MATIC.
- `TxnFee(USD)`: Transaction fee in USD.
- `Historical $Price/MATIC`: Historical price of MATIC (which may have missing values that need filling).

## Key Steps in Data Cleaning

1. **Column Name Cleanup**: Spaces in column names are replaced with underscores for easier handling.
    ```python
    df.columns = df.columns.str.replace(' ', '_')
    ```

2. **Handling Missing Data**: Missing values in `Historical_$Price/MATIC` are filled based on a calculation using other columns in the dataset.

    ```python
    filtered_date_hist = df[df["DateTime_(UTC)"] >= "2024-04-16"]
    df.loc[filtered_date_hist.index, "Historical_$Price/MATIC"] = filtered_date_hist["CurrentValue_@_$0.703172221747878/MATIC"] / filtered_date_hist["Value_IN(MATIC)"]
    df = df.dropna(subset=["Historical_$Price/MATIC"])
    ```

3. **Data Filtering**: Data is filtered by date (`DateTime_(UTC)`) to ensure that only relevant records are used for specific calculations.

## Visualizations

The project uses both `matplotlib` and `plotly` to generate visualizations that explore trends in the MATIC transaction data.

- **Matplotlib**: Used for basic plots like line charts and bar charts.
- **Plotly**: Interactive visualizations that allow for a more dynamic exploration of the data.

## Dependencies

The following Python libraries are used in the project:

- `pandas`: For data manipulation and analysis.
- `matplotlib`: For static visualizations.
- `plotly.express`: For interactive visualizations.

Install these dependencies via `pip`:

```bash
pip install pandas matplotlib plotly
```

## Running the Project

1. Clone this repository.
2. Ensure the dataset (`polygon.csv`) is available in the root directory of the project.
3. Open the `datacleaning.ipynb` file in Jupyter Notebook.
4. Run the cells sequentially to clean the dataset and perform analysis.