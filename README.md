# King County House Sales Analysis Dashboard

This project analyzes house sales in King County, Washington, using a combination of SQL, Python, and Tableau. It transforms raw public data into actionable insights for real estate stakeholders.

## Project Overview

- **Data Source:** [King County House Sales (Public Data)](https://www.kaggle.com/datasets/harlfoxem/housesalesprediction)
- **Visualization:** [Interactive Tableau Dashboard](https://public.tableau.com/app/profile/neelam.s.jat/viz/KingCountyHouseSales_17581165566070/KingCountyHouseSales)
- **Tech Stack:** SQL (data cleaning/filtering), Python (preprocessing), Tableau (visualization)

---

## Business Questions Answered

1. **What is the daily average house sale price in King County for July 2014?**
2. **How are house prices distributed across different price ranges?**
3. **Which neighborhoods or regions are most active in house sales?**
4. **How do property features (bedrooms, bathrooms, square footage) relate to sale price?**
5. **What is the impact of house condition and view on sale price?**
6. **What are the most common property characteristics (year built, lot size, etc.)?**
7. **How can buyers and sellers identify typical home profiles and market trends?**

---

## Project Flow

1. **Data Acquisition**
   - Downloaded the public dataset from Kaggle.
   - Verified source and integrity.

2. **Data Cleaning and Preparation**
   - Used SQL to filter, join, and aggregate key columns.
   - Employed Python for handling missing values and feature engineering.

3. **Exploratory Data Analysis**
   - Identified outliers and common ranges for price, bedrooms, bathrooms, lot size, and living area.

4. **Dashboard Creation in Tableau**
   - Built interactive visualizations for price distribution, sales trend, feature breakdowns, and spatial analysis.
   - Published dashboard for public access.

---

## SQL Scripts

```sql name=king_county_clean.sql
-- Filter dataset to July 2014, remove nulls, and select key columns
SELECT id, date, price, bedrooms, bathrooms, sqft_living, sqft_lot, floors, waterfront,
       view, condition, grade, yr_built, zipcode, lat, long
FROM house_sales
WHERE date >= '2014-07-01' AND date < '2014-08-01'
  AND price IS NOT NULL
  AND bedrooms IS NOT NULL
  AND bathrooms IS NOT NULL
  AND sqft_living IS NOT NULL
  AND zipcode IS NOT NULL;
```

---

## Python Scripts

```python name=preprocess_king_county.py
import pandas as pd

# Load the cleaned CSV from SQL query
df = pd.read_csv("king_county_clean.csv")

# Convert date to datetime
df['date'] = pd.to_datetime(df['date'])

# Handle missing values for features (fill with median or drop)
for col in ['sqft_lot', 'view', 'condition', 'grade']:
    if df[col].isnull().sum() > 0:
        df[col].fillna(df[col].median(), inplace=True)

# Feature engineering: add price per sqft
df['price_per_sqft'] = df['price'] / df['sqft_living']

# Remove extreme outliers in price
df = df[df['price'] < 2000000]

# Save for Tableau
df.to_csv("king_county_preprocessed.csv", index=False)
```

---

## Tableau Dashboard

- **Filters:** Month, year built, sqft living, sqft lot
- **Visuals:** Daily average sales price, map of sales, price distribution, view vs condition heatmap, bathroom and bedroom distribution
- **Link:** [King County House Sales Tableau Dashboard](https://public.tableau.com/app/profile/neelam.s.jat/viz/KingCountyHouseSales_17581165566070/KingCountyHouseSales)

---

## Usage

1. Run the SQL script to extract and clean raw data.
2. Use the Python script for further preprocessing and feature engineering.
3. Import the processed CSV into Tableau.
4. Explore the dashboard and answer business questions.

---

## License

**License: MIT License**

This project is open source under the MIT License. You are free to use, modify, and distribute it, provided that the original source and contributors are credited.

```
MIT License

Copyright (c) 2025 Neelam-jat

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:
...
```

---

## Contact

For feedback, contributions, or questions, please reach out via [GitHub Issues](https://github.com/Neelam-jat/) or connect on Tableau Public.
