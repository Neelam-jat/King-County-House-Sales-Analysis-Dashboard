# King County House Sales Tableau Project

This repository provides a comprehensive analysis and interactive dashboard of house sales in King County, Washington, spanning multiple years. The project leverages SQL and Python for data cleaning and preprocessing, and Tableau for visualization. It is designed to deliver actionable insights to buyers, sellers, and real estate professionals.

---

## 🖼️ Dashboard Preview

![King County House Sales Board Preview](King%20County%20House%20Sales%20Board%20.png)

For a live, interactive view, access the dashboard here:  
[King County House Sales Tableau Dashboard](https://public.tableau.com/app/profile/neelam.s.jat/viz/KingCountyHouseSales_17581165566070/KingCountyHouseSales)

---

## 📊 Project Flow

1. **Data Review**
    - Inspect the raw Excel data (`HouseData.xlsx`) to understand available features (price, bedrooms, bathrooms, sqft, year built, etc.).

2. **Data Preparation**
    - **SQL**: Clean, filter, and select relevant records across all available years, remove nulls, and aggregate key columns.

SQL script:
    ```sql
    -- Select and clean data across all years, remove nulls
    SELECT id, date, price, bedrooms, bathrooms, sqft_living, sqft_lot, floors, waterfront,
           view, condition, grade, yr_built, zipcode, lat, long
    FROM house_sales
    WHERE price IS NOT NULL
      AND bedrooms IS NOT NULL
      AND bathrooms IS NOT NULL
      AND sqft_living IS NOT NULL
      AND zipcode IS NOT NULL;
    ```

    - **Python**: Handle missing values, engineer new features (e.g., price per sqft), and remove outliers.

 Python script:
    ```python
    import pandas as pd

    df = pd.read_excel("HouseData.xlsx")
    df['date'] = pd.to_datetime(df['date'])
    for col in ['sqft_lot', 'view', 'condition', 'grade']:
        if df[col].isnull().sum() > 0:
            df[col].fillna(df[col].median(), inplace=True)
    df['price_per_sqft'] = df['price'] / df['sqft_living']
    df = df[df['price'] < 2000000]
    df.to_csv("king_county_preprocessed.csv", index=False)
    ```

3. **Tableau Visualization**
    - Import the cleaned data into Tableau.
    - Build interactive visuals:
        - Filter by month/year, living area, lot size.
        - Daily average house sales price by selected month/year.
        - Map of sales by region.
        - Distribution of house prices, bedrooms, bathrooms.
        - View vs condition heatmap with average prices.
    
4. **Review & Usage**
    - Refer to the screenshot (`King County House Sales.png`) for a quick overview.
    - Open the Tableau workbook (`KingCountyHouseSales_Dashboard.twbx`) for full interactivity.

---

## 💼 Business Questions & Answers

**1. How do house sales and prices change across different months and years?**
   - The dashboard allows users to filter by month and year. Average house prices fluctuate over time, with some months showing higher average prices, e.g., May 2014 peaked near $600,000.

**2. What is the distribution of house prices in King County?**
   - Most houses are sold in the $200,000–$700,000 range. High-priced sales ($1M+) are less frequent.

**3. Which regions have the highest sales and prices?**
   - The Seattle metropolitan area and north King County show higher sales activity and prices, as illustrated by the interactive map.

**4. How do property features (bedrooms, bathrooms, living area) relate to sale price?**
   - Most homes have 3–4 bedrooms, 2–3 bathrooms, and living areas between 1,000–3,000 sqft.
   - More bedrooms and bathrooms generally correlate with higher prices, but outliers exist.

**5. How do house condition and view affect sale prices?**
   - The View vs Condition heatmap shows:
     - Houses with "Very Good" conditions and "Excellent" views fetch the highest average prices (often above $1M).
     - "No View" properties have lower average prices, regardless of condition.
     - Condition upgrades add significant value, especially for houses with a view.

**6. How does lot size and living area impact sales?**
   - Larger living areas and lot sizes correspond to higher prices, but most sales fall within moderate ranges (living area < 3,000 sqft, lot < 10,000 sqft).

**7. Are there seasonal or market trends visible in the data?**
   - Yes, the dashboard’s time filter reveals that certain months (e.g., May, July) have higher average prices and sales volume, indicating possible seasonal effects.

---

## 📝 License

This project is licensed under the MIT License. See the LICENSE file for details.

---

## ✨ Getting Started

1. Clone the repository and review `HouseData.xlsx` for source data.
2. Use provided SQL and Python scripts for cleaning and preprocessing.
3. Open `KingCountyHouseSales_Dashboard.twbx` in Tableau Desktop or Tableau Public.
4. Explore the dashboard and refer to the PNG screenshot or the online Tableau link for a preview.

---

## 📬 Contact

For feedback, contributions, or questions, please reach out via [GitHub Issues](https://github.com/Neelam-jat/) or connect on Tableau Public.
