# Energy Data Extraction and MongoDB Storage (2000–2024)

## Overview
This project extracts **energy-related data for African countries (2000–2024)** from the **Africa Energy Portal (AEP)**, formats it according to a standard schema, and stores it in **MongoDB**.  

It was completed as part of the **Internship Week 1** task on *Energy Data Extraction and MongoDB Storage*.  

---

## Project Workflow

### 1. **Data Collection**
- The data was obtained manually from the **[Africa Energy Portal](https://africa-energy-portal.org/)**.
- After selecting the desired indicators, the **developer tools → Network → Response** tab was used to view the API response in JSON format.
- The JSON data was **copied**, **pasted into Notepad**, and **saved as `.json` files**.
- These files were then processed in Python.

---

### 2. **Data Processing Steps (Notebook Explanation)**

| Step | Description |
|------|--------------|
| **1. Import Libraries & Load Data** | Used `glob` to load all JSON files and combine them into one dataset. |
| **2. Rename Columns** | Standardized all field names to match internship schema (country, metric, sector, etc.). |
| **3. Clean Data** | Converted text-based numeric fields (like “N/A”) to proper numbers. |
| **4. Pivot Table** | Transformed rows into a wide format where each column represents a year (2000–2024). |
| **5. Save Final CSV** | Exported processed data as `africa_energy_data.csv` ready for database insertion. |

---

### 3. **Expected Data Format**

| country | country_serial | metric | unit | sector | sub_sector | source_link | source | 2000 | 2001 | ... | 2024 |
|----------|----------------|--------|------|---------|-------------|-------------|--------|------|------|-----|------|
| Kenya | KE | Electricity generation | GWh | Energy | Electricity | https://africa-energy-portal.org | AEP | 4500 | 4600 | ... | 9200 |

---

## MongoDB Storage

After processing and exporting the final dataset (africa_energy_data.csv), the data was inserted into a MongoDB collection.
Each record represents one energy metric for a single country across the years 2000–2024, following the same schema used in the CSV.

The MongoDB collection structure mirrors the columns of the CSV file, with text fields for descriptive data (e.g., country, metric, unit) and numeric fields for each year’s values.

Example document:
```
{
  "country": "Kenya",
  "metric": "Electricity access",
  "unit": "%",
  "sector": "Energy",
  "source": "AEP",
  "2000": 36.5,
  "2001": 38.2,
  "...": "...",
  "2024": 75.1
}
```

## Validation & Checks

| Check | Description |
|-------|--------------|
| **Missing Years** | Verified coverage for 2000–2024. Any missing years were recorded. |
| **Consistency** | Ensured unit names and country names are standardized. |
| **Data Types** | Confirmed all year values are numeric. |

---

## Technologies Used
- **Python** (pandas, json, glob)
- **MongoDB** (NoSQL database)
- **Africa Energy Portal** (Data source)

---

## Author
**Lucy Joan**  
Intern – Lux Academy  

---

