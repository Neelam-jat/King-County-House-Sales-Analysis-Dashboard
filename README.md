# King County House Sales Tableau Project

This repository provides a comprehensive analysis and interactive dashboard of house sales in King County, Washington, for July 2014. The project leverages SQL and Python for data cleaning and preprocessing, and Tableau for visualization. It is designed to deliver actionable insights to buyers, sellers, and real estate professionals.

---

## 📂 Project Files

- **HouseData.xlsx**: Original raw dataset of King County house sales.
- **King County House Sales.png**: Screenshot of the Tableau dashboard (quick overview).
- **KingCountyHouseSales_Dashboard.twbx**: Tableau workbook file containing the interactive dashboard.
- **LICENSE**: Project license (MIT).
- **README.md**: This documentation.

---

## 🖼️ Dashboard Preview

![Dashboard Screenshot](King%20County%20House%20Sales.png)

For a live, interactive view, access the dashboard here:  
[King County House Sales Tableau Dashboard](https://public.tableau.com/app/profile/neelam.s.jat/viz/KingCountyHouseSales_17581165566070/KingCountyHouseSales)

---

## 📊 Project Flow

1. **Data Review**
    - Inspect the raw Excel data (`HouseData.xlsx`) to understand available features (price, bedrooms, bathrooms, sqft, year built, etc.).

2. **Data Preparation**
    - **SQL**: Filter, clean, and select relevant records for July 2014, remove nulls, and aggregate key columns.
    - **Python**: Handle missing values, engineer new features (e.g., price per sqft), and remove outliers.

    Example SQL script:
    ```sql
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

    Example Python script:
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
        - Daily average house sales price
        - Map of sales by region
        - Distribution of house prices, bedrooms, bathrooms
        - View vs condition heatmap
        - Filters for month, year built, sqft living, and lot size

4. **Review & Usage**
    - Refer to the screenshot (`King County House Sales.png`) for a quick overview.
    - Open the Tableau workbook (`KingCountyHouseSales_Dashboard.twbx`) for full interactivity.

---

## 💡 Business Questions & Answers

**1. What is the daily average house sale price in King County for July 2014?**
   - The daily average price fluctuates around $500,000, showing a stable market during the month.

**2. How are house prices distributed?**
   - Most houses are sold in the $200,000–$700,000 range, with fewer sales above $1 million.

**3. Which areas see the most house sales?**
   - The Seattle metropolitan region shows higher sales activity, as seen on the map.

**4. What are the most common property features?**
   - Most homes have 3–4 bedrooms and 2–3 bathrooms; living area typically ranges from 1,000–3,000 sqft.

**5. How do condition and view impact sales?**
   - Houses with "No View" and average conditions are most common. "Good" or "Excellent" views are rare and likely command higher prices.

**6. Are there seasonal or daily trends?**
   - No drastic daily price changes in July 2014, indicating consistent buyer activity.

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
