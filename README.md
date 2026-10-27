# Customer Data Cleaning with Python & Pandas

A beginner-friendly Python project that cleans and validates a messy customer dataset using Pandas, NumPy, regular expressions, and date parsing. The goal is to make customer data more consistent and suitable for further analysis.

## Project Overview

The raw dataset contains common data-quality issues, including missing values, inconsistent formatting, invalid email addresses, differently formatted phone numbers and dates, spelling variations, and non-standardized categorical values.

This project walks through inspecting the dataset, applying field-specific cleaning rules, validating the results, and exporting a cleaned CSV file.

## Dataset

The project uses a customer dataset with **538 original records** and these columns:

| Column | Description |
|---|---|
| `customer_id` | Customer identifier |
| `first_name` | Customer's first name |
| `last_name` | Customer's last name |
| `email` | Customer email address |
| `phone` | Customer phone number |
| `gender` | Customer gender |
| `birth_date` | Customer date of birth |
| `registration_date` | Customer registration date |
| `country` | Customer country |
| `city` | Customer city |
| `address` | Customer address |
| `is_active` | Customer account status |
| `notes` | Additional customer notes |

## What the Project Does

### 1. Data inspection
- Reviews dataset dimensions, data types, missing values, unique values, value distributions, and duplicate records.
- Removes rows that are completely empty.

### 2. Customer IDs and names
- Converts `customer_id` to an integer and checks for duplicate IDs.
- Trims whitespace, collapses repeated spaces, and standardizes name capitalization.
- Does not treat repeated first or last names as duplicate customers.

### 3. Email validation
- Trims whitespace and converts email addresses to lowercase.
- Uses a regular expression to check email structure.
- Adds an `email_valid` indicator to identify email values that match the validation pattern.
- Inspects duplicate email addresses without automatically deleting customer records.

### 4. Country and city standardization
- Trims and standardizes text values.
- Maps known spelling variations and alternate representations to consistent country and city names.

### 5. Phone-number cleaning
- Checks phone-number formats and lengths.
- Identifies values containing letters and extracts numeric characters as part of the cleaning process.
- Handles empty or invalid values and removes the international `00` prefix where applicable.
- Keeps phone numbers as strings because they are identifiers, not quantities.

### 6. Gender and account status
- Standardizes gender values into categories such as `male`, `female`, `other`, and `unknown` where applicable.
- Normalizes common active/inactive representations such as `yes`, `y`, `true`, `1`, `no`, `n`, `false`, and `0`.

### 7. Notes and addresses
- Trims whitespace and normalizes text.
- Converts empty or placeholder notes such as `-`, `unknown`, `n/a`, and `null` to missing values.
- Standardizes whitespace in address values.

### 8. Date cleaning and validation
- Parses multiple formats in `birth_date` and `registration_date`.
- Handles missing, placeholder, and invalid dates.
- Applies validation rules for unrealistic birth years, registration dates before 2000, and future registration dates.

### 9. Final data-quality checks
- Checks data types, missing values, duplicate rows, duplicate customer IDs, and categorical values.
- Inspects repeated email addresses, phone numbers, and addresses rather than assuming that repeated values always indicate duplicate customers.

## Workflow

```text
Raw customer dataset
        ↓
Inspect dataset and data quality
        ↓
Remove completely empty rows
        ↓
Clean customer IDs and names
        ↓
Validate email addresses
        ↓
Clean phone numbers
        ↓
Standardize countries and cities
        ↓
Standardize gender and account status
        ↓
Clean notes, dates, and addresses
        ↓
Run final data-quality checks
        ↓
Export the cleaned CSV
```

## Technologies Used

- Python
- Pandas
- NumPy
- Regular expressions (Regex)
- `python-dateutil`
- Jupyter Notebook

## Repository Structure

```text
customer-data-cleaning/
├── customers_dirty.csv
├── customers_clean.csv
├── customer_cleaning.ipynb
└── README.md
```

| File | Description |
|---|---|
| `customers_dirty.csv` | Original customer dataset |
| `customers_clean.csv` | Cleaned output dataset exported by the notebook |
| `customer_cleaning.ipynb` | Notebook containing the data inspection and cleaning workflow |
| `README.md` | Project documentation |

## How to Run

### 1. Clone the repository

```bash
git clone https://github.com/suhas2357/customer-data-cleaning.git
cd customer-data-cleaning
```

### 2. Install dependencies

```bash
python -m pip install pandas numpy python-dateutil jupyter
```

### 3. Check the input CSV path

The notebook currently reads the input from `clean/customers_dirty.csv`:

```python
customers = pd.read_csv('clean/customers_dirty.csv')
```

In the repository structure above, `customers_dirty.csv` is in the project root. To run the notebook from that structure without moving the file, change the input line to:

```python
customers = pd.read_csv('customers_dirty.csv')
```

Alternatively, create a `clean` folder and place `customers_dirty.csv` inside it.

### 4. Run the notebook

```bash
jupyter notebook
```

Open `customer_cleaning.ipynb` and run the cells from top to bottom. The notebook exports the cleaned data to `customers_clean.csv` in the current working directory.

## Key Learning Outcomes

This project demonstrates that data cleaning should account for the meaning of each field. Repeated names, addresses, phone numbers, or email addresses do not automatically prove that two customer records are duplicates. The notebook emphasizes inspecting values, applying explicit cleaning rules, and checking data quality after transformations.

Skills practiced include:

- Data inspection and cleaning
- Missing-value handling
- Duplicate detection
- String manipulation and regular expressions
- Date parsing and validation
- Data-type conversion
- Categorical-value standardization
- Pandas DataFrame operations
- Exporting processed data to CSV

## Future Improvements

- Recreate selected cleaning steps using SQL.
- Add automated data-quality tests.
- Perform exploratory data analysis (EDA).
- Create visualizations or a Power BI dashboard.
- Turn the notebook into a reusable data-cleaning pipeline.

## Project Status

**Status:** Initial data-cleaning portfolio project.

## Author

**Suhas Sonwane**

- GitHub: [@suhas2357](https://github.com/suhas2357)
- Repository: [customer-data-cleaning](https://github.com/suhas2357/customer-data-cleaning)
