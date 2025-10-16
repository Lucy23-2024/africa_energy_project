# 🌍 Energy Data Extraction and MongoDB Storage (2000–2024)

## 📘 Overview
This project extracts **energy-related data for African countries (2000–2024)** from the **Africa Energy Portal (AEP)**, formats it according to a standard schema, and stores it in **MongoDB**.  

It was completed as part of the **Internship Week 1** task on *Energy Data Extraction and MongoDB Storage*.  

---

## 🗂️ Project Structure
```
AFRICA_ENERGY_PROJECT/
│
├── venv/                         # Virtual environment folder
├── .gitignore                    # Files and folders to ignore in GitHub
├── .python-version               # Python version configuration
├── africa_energy_data.ipynb      # Main Jupyter Notebook (data processing workflow)
├── africa_energy_data.csv        # Final processed dataset (ready for MongoDB)
├── electricity.json              # Raw JSON data (electricity indicators)
├── energy.json                   # Raw JSON data (energy indicators)
├── social_and_economic.json      # Raw JSON data (social and economic indicators)
├── main.py                       # Optional script version of notebook logic
├── pyproject.toml                # Python project dependencies/config
└── README.md                     # Project documentation (this file)
```

💡 *Note:* The `.json` files are the manually downloaded datasets from the Africa Energy Portal.  
They are combined and cleaned within the Jupyter notebook.

---

## 🧩 Project Workflow

### 1. **Data Collection**
- Data was obtained manually from the **[Africa Energy Portal](https://africa-energy-portal.org/)**.
- Using browser developer tools, the **Network → Response** tab revealed API responses in JSON format.
- The JSON data was **copied**, **saved in Notepad**, and stored as `.json` files.
- These files were then processed using Python.

---

### 2. **Data Processing Steps**

| Step | Description |
|------|--------------|
| **1. Import Libraries & Load Data** | Used `glob` to load all JSON files and combine them into one dataset. |
| **2. Rename Columns** | Standardized field names to match the internship schema. |
| **3. Clean Data** | Converted non-numeric fields like `"N/A"` to proper numbers. |
| **4. Pivot Table** | Transformed data so each year (2000–2024) became a column. |
| **5. Save Final CSV** | Exported the cleaned dataset as `africa_energy_data.csv` ready for MongoDB. |

---

### 3. **Expected Data Format**

| country | country_serial | metric | unit | sector | sub_sector | source_link | source | 2000 | 2001 | ... | 2024 |
|----------|----------------|--------|------|---------|-------------|-------------|--------|------|------|-----|------|
| Kenya | KE | Electricity generation | GWh | Energy | Electricity | /aep/country/kenya | AEP | 4500 | 4600 | ... | 9200 |

---

## 🗄️ MongoDB Storage

After exporting the cleaned dataset (`africa_energy_data.csv`), it was inserted into a **MongoDB** collection.  
Each record represents **one energy metric for one country** across the years 2000–2024.

The MongoDB collection mirrors the CSV structure — with text fields for identifiers and numeric fields for each year.

### Example Document
```json
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

---

## ✅ Validation & Checks

| Check | Description |
|-------|--------------|
| **Missing Years** | Verified coverage for all years (2000–2024). |
| **Consistency** | Standardized country names and units. |
| **Data Types** | Ensured numeric values are correctly formatted. |

---

## 🧰 Technologies Used
- **Python** → `pandas`, `json`, `glob`
- **MongoDB** → NoSQL database for data storage
- **Africa Energy Portal** → Primary data source

---

## 👩🏽‍💻 Author
**Lucy Joan**  
Intern – Lux Academy  
