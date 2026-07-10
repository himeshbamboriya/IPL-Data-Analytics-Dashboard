# IPL-Data-Analytics-Dashboard
An end-to-end data analytics project using Power Query and Excel Data Models to analyze 16 years of IPL cricket data.
<div align="center">

# 🏏 IPL Cricket Analytics Dashboard (2008-2024)

[Excel](https://img.shields.io/badge/Microsoft_Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![Power Query](https://img.shields.io/badge/Power_Query-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Data Analysis](https://img.shields.io/badge/Data_Analytics-FF6F00?style=for-the-badge&logo=google-analytics&logoColor=white)

</div>

---

## 📖 Project Overview
This project analyzes 16 years of Indian Premier League (IPL) cricket data, containing over 250,000 individual ball-by-ball deliveries. The goal of this analysis is to evaluate franchise performance, specifically focusing on Royal Challengers Bengaluru (RCB), by breaking down match-phase metrics and testing common cricket assumptions like the "toss advantage."

---

## 🛠️ Data Processing & Methodology

Working with a dataset of this size in standard Excel presented immediate technical challenges. Attempting to join the 1,000-row match table with the 250,000-row delivery table using standard `XLOOKUP` functions resulted in memory exhaustion and system freezing. 

To resolve this and build a stable, optimized file, the following steps were taken:

1. **ETL via Power Query:** Imported the raw CSV files into Power Query to clean empty strings natively. Standardized older franchise names (e.g., changing "Royal Challengers Bangalore" to "Royal Challengers Bengaluru").
2. **Memory-Efficient Merging:** Executed a Left Outer Join within Power Query to merge the match outcomes with the ball-by-ball data, bypassing the spreadsheet grid entirely to prevent RAM overload.
3. **The Data Model Engine:** Loaded the cleaned 250k+ rows directly into Excel's Data Model. This allowed for the use of the `Distinct Count` feature, ensuring that match-level metrics (like win percentages) were calculated accurately without being skewed by the ball-by-ball row count.
4. **Feature Engineering:** Created a conditional `Match Phase` column to categorize raw ball numbers into standard cricket phases: *Powerplay* (Overs 1-6), *Middle Overs* (Overs 7-15), and *Death Overs* (Overs 16-20).

---

## 📊 Key Questions Answered

Inspired by standard exploratory data analysis, this dashboard was built to answer three specific business questions:

**Q1: Does winning the toss and electing to field actually provide a significant advantage for RCB?**
* **Analysis:** By utilizing the Data Model's Distinct Count on the Match ID, the data shows that the perceived massive advantage of chasing is actually quite balanced. 
* **Result:** When RCB wins the toss and chooses to field, their historical win rate normalizes to **50.59%**.

**Q2: Who are the most consistent run-scorers for the franchise across different seasons?**
* **Analysis:** Aggregated the `runs_scored` column by individual strikers. 
* **Result:** The dashboard features a dynamic bar chart that updates via a Season Slicer, allowing users to track peak performer consistency from 2008 to 2024.

**Q3: Which bowlers are the most effective during the crucial "Death Overs"?**
* **Analysis:** Filtered the data using the newly engineered `Match Phase` column to isolate balls bowled in overs 16-20, then summed the `wicket_confirmation` boolean.
* **Result:** Isolated the top 10 most effective wicket-takers in the final 5 overs to identify reliable match-finishers.

---

## 🖥️ Dashboard Interface

<div align="center">
  <img src=https://github.com/himeshbamboriya/IPL-Data-Analytics-Dashboard/blob/main/Excel_dashboard.png?raw=true alt="IPL Dashboard" width="800"/>
</div>

### Interactive Features
- **Dynamic Season Slicer:** Instantly filters all charts by specific IPL years using Report Connections.
- **KPI Scorecards:** Real-time staging cells tracking Total Matches, Total Runs, and Total Wickets across the filtered parameters.

---

## 🗃️ Data Dictionary

<details>
<summary>Click to expand dataset details</summary>

| Column Name | Description | Data Type |
| :--- | :--- | :--- |
| `Match_id` | Unique identifier for each IPL match | Integer |
| `Innings` | 1st or 2nd innings indicator | Integer |
| `Batting_team` | Standardized name of the batting franchise | String |
| `Match Phase` | Custom feature: Powerplay, Middle, or Death Overs | String |
| `Runs_scored` | Runs scored on that specific delivery | Integer |
| `Wicket_confirmation` | Boolean indicator (1 = Wicket, 0 = Safe) | Integer |

</details>

---

## 🚀 How to Run This Project

1. Download the **`IPL_Analytics_Master.xlsb`** file directly from this repository. 
2. Open in Microsoft Excel (2016 or newer recommended).
3. Ensure macros/content are enabled to allow the Data Model to calculate.
4. Navigate to the **Dashboard** tab and use the Slicer panel on the left to explore the data.
