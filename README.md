# 📊 Macroeconomic Outlook 2025.1: Fiscal Section

> **Official repository for the fiscal analysis developed for the Macroeconomic Outlook report by the IbMacro student-led league.**

[![R](https://img.shields.io/badge/Made_with-R-blue?style=for-the-badge&logo=R)](https://www.r-project.org/)
[![Data Source](https://img.shields.io/badge/Data-IMF%20%26%20World%20Bank-orange?style=for-the-badge)](https://www.imf.org/en/Data)
[![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)]()

## 👥 Authors
* **João Abdo**
* **João Moreno**
* **Lauro Aguiar**

---

## 🎯 Project Objective

This project focuses on analyzing **fiscal sustainability** and **public spending efficiency** in Brazil, comparing it with regional peers (Latin America) and economic blocs (BRICS and Developed Countries). 

The analysis goes beyond conventional metrics by examining not only *how much* is spent, but the *quality* of that spending, developing proprietary indicators based on microdata.

---

## 🛠 Methodology and Technical Approach

The fiscal section was built using a **data-driven** approach, automating the collection and processing of large international datasets.

### 1. Automated Data Collection (APIs)
Instead of downloading static spreadsheets, we developed **R** scripts to connect directly to the APIs of multilateral institutions:
* **IMF (IMF DataMapper API):** For macro-fiscal data (Gross Debt, Primary Balance, Revenues, and Expenditures) for Latin American countries (`BRA`, `ARG`, `CHL`, `COL`, `PRY`, `PER`, `MEX`, `URY`).
* **World Bank (WBStats):** For socioeconomic indicators used in efficiency calculations.
* **Global Macro Database (GMD):** For long historical series and structural comparisons.

### 2. Public Spending Efficiency Index (Custom Index)
A key differentiator of this work was the creation of a **Quality of Public Goods Index**. We used the `wbstats` library to aggregate indicators across 5 dimensions:

* 📚 **Education:** Literacy rates, PISA scores, and secondary education completion.
* 🏥 **Health:** Life expectancy and neonatal mortality.
* ⚖️ **Administration:** Corruption control, judicial quality, and bureaucracy.
* 🤝 **Equity:** Income share of the bottom 40%.
* ⚡ **Infrastructure:** Access to electricity and public safety.

> **Efficiency Formula:**
> 
> $$\text{Efficiency} = \frac{\text{Public Goods Quality Index}}{\text{Public Spending \% of GDP)}}$$

---

## 📈 Key Findings (Highlights)

The code generates visualizations that address the following questions:
1. **Sustainability:** Is Brazil's Gross Debt trajectory explosive compared to its LATAM peers?
2. **Fiscal Result:** How does Brazil’s *Net Lending/Borrowing* behave amidst regional volatility?
3. **Cost-Benefit:** Does Brazil overspend? Does this spending translate into public goods of comparable quality to OECD or BRICS countries?

---

## 💻 Code Structure

Below is a simplified example of how we structured the IMF data extraction to ensure reproducibility:

```r
# Example of IMF API extraction used in the project
fetch_indicator <- function(indicator_id) {
  base_url <- "[https://www.imf.org/external/datamapper/api/v1](https://www.imf.org/external/datamapper/api/v1)"
  url <- sprintf("%s/%s/%s?periods=%s", base_url, indicator_id, paste(countries, collapse = "/"), periods_param)
  
  resp <- GET(url)
  # ... (JSON processing and cleaning) ...
  return(data_indicator)
}
```
--- 
This is an academic and educational project developed under IbMacro.
