# 🔐 **Vulnerability Scorecard — Power BI Dashboard**

A comprehensive **Vulnerability Management & Exposure Analytics Scorecard** built in **Power BI** to help cybersecurity teams monitor risk posture, vulnerability severity, remediation performance, and asset exposure across the organization.

🔗 **Live Dashboard (HTML View):**
[https://atsuvovor.github.io/power_bi_projects/cyber_attack_insight_dashboard.html](https://atsuvovor.github.io/power_bi_projects/cyber_attack_insight_dashboard.html)

📁 **Part of the Cyber Attack Insight Dashboard Collection**

---

## 📌 **Overview**

The **Vulnerability Scorecard** transforms raw vulnerability scan data into an interactive, executive-ready reporting view.
It centralizes risk indicators across:

* Vulnerability severity levels
* Exposure by asset and business unit
* CVE distribution
* Remediation performance
* High-risk vs critical trends

This scorecard enables security leaders, SOC teams, and risk management functions to make **faster, evidence-backed decisions** on where to prioritize remediation and resources.

---

## 🖼️ **Dashboard Preview (Screenshots)**

> *(Upload your screenshots and I will replace the placeholders for you)*

```
![Vulnerability Scorecard Overview](images/vulnerability_scorecard_overview.png)
![Severity Distribution](images/vulnerability_severity_distribution.png)
![Asset Exposure](images/asset_exposure.png)
![Remediation Performance](images/remediation_performance.png)
```

---

## 🎯 **Business Objectives**

The Vulnerability Scorecard is designed to solve key challenges:

* Identifying **high & critical vulnerabilities** needing urgent remediation
* Understanding **asset and business-unit exposure**
* Visualizing **remediation backlog** and performance
* Prioritizing risks using severity, exploitability, and criticality
* Providing **executive-level risk insights** aligned to risk appetite
* Tracking vulnerability volume trends over time

---

## 🧠 **Key Features**

### ✔️ Severity-Level Metrics

* Critical, High, Medium, and Low vulnerabilities
* Severity breakdown using stacked bar and donut charts

### ✔️ High-Risk Exposure Mapping

* Asset exposure by host, business unit, or application
* Ability to filter by severity, CVE, or detection source

### ✔️ CVE Distribution & Threat Context

* CVE frequency visualization
* Shows recurring or systemic vulnerability patterns

### ✔️ Remediation Performance

* Average remediation time
* SLA breaches
* Backlog volume trends

### ✔️ Executive Scorecard View

* Total vulnerabilities
* Critical & high counts
* Exposure score
* SLA compliance metrics

---

## 🧬 **Data Inputs & Data Model**

The Vulnerability Scorecard uses a star-schema design:

### **Fact Table**

* `FactVulnerabilities`

  * CVE
  * Severity
  * Detection Source
  * Asset ID
  * First Detected Date
  * Last Observed Date
  * Remediation Date
  * Status (Open/Closed)
  * CVSS Score

### **Dimension Tables**

* `DimSeverity`
* `DimAssets`
* `DimBusinessUnit`
* `DimDetectionSource`
* `DimCVE`

### **Power Query Transformations**

* Standardized severity levels
* Normalized asset naming
* Extracted dates & time attributes
* Combined multiple scanner sources
* Removed duplicates / false positives

---

## 📐 **DAX Formulas Used**

### **1. Total Vulnerabilities**

```DAX
Total Vulnerabilities =
COUNTROWS(FactVulnerabilities)
```

### **2. Critical Vulnerabilities**

```DAX
Critical Vulnerabilities =
CALCULATE(
    COUNTROWS(FactVulnerabilities),
    FactVulnerabilities[Severity] = "Critical"
)
```

### **3. Exposure Score**

```DAX
Exposure Score =
SUMX(
    FactVulnerabilities,
    FactVulnerabilities[CVSS_Score] * RELATED(DimAssets[Asset_Criticality])
)
```

### **4. SLA Compliance**

```DAX
SLA Compliance % =
DIVIDE(
    [Vulnerabilities Resolved Within SLA],
    [Total Resolved Vulnerabilities]
)
```

### **5. Backlog Count**

```DAX
Open Vulnerability Backlog =
CALCULATE(
    COUNTROWS(FactVulnerabilities),
    FactVulnerabilities[Status] = "Open"
)
```

---

## 📊 **KPIs Provided**

| KPI                                 | Description                                    |
| ----------------------------------- | ---------------------------------------------- |
| **Total Vulnerabilities**           | Overall exposure volume                        |
| **Critical & High Vulnerabilities** | Highest-risk items requiring rapid remediation |
| **Mean Time To Remediate (MTTR)**   | Effectiveness of remediation processes         |
| **Backlog Volume**                  | Outstanding vulnerabilities                    |
| **Exposure Score**                  | Weighted risk measure using CVSS + criticality |
| **Top Affected Assets**             | Identifies most at-risk systems                |

---

## 🗂️ Folder Structure (Recommended)

```
vulnerability_scorecard/
│
├── README.md
├── Vulnerability_Scorecard.pbix
├── images/
│   ├── vulnerability_scorecard_overview.png
│   ├── vulnerability_severity_distribution.png
│   ├── asset_exposure.png
│   └── remediation_performance.png
├── data/
│   ├── sample_vulnerability_data.csv
│   └── data_dictionary.md
└── docs/
    ├── model_schema.pdf
    ├── dax_reference.md
    └── methodology.md
```

---

## 📘 **Methodology**

### **Step 1: Ingest Data**

* Export from vulnerability scanner (Nessus, Qualys, Tenable, etc.)
* Load into Power Query

### **Step 2: Clean + Transform**

* Normalize severity
* Correct inconsistent asset IDs
* Identify duplicates
* Generate time intelligence fields

### **Step 3: Build Data Model**

* Configure one-to-many relationships
* Build time table
* Add severity weighting logic

### **Step 4: Create DAX Measures**

* Risk scoring
* SLA compliance
* Severity filters
* Backlog counters

### **Step 5: Design UX**

* Executive-first design
* Severity color standards (red/orange/yellow/blue)
* Drill-through enabled
* Bookmark navigation

---

## 🎯 **Use Cases**

* SOC threat monitoring
* Vulnerability management
* Patch governance
* Executive cyber risk reporting
* Audit & compliance communications
* Prioritization of remediation tasks

---

## 💼 **Target Stakeholders**

* Cybersecurity Teams
* Vulnerability Managers
* Security Engineering
* IT Operations
* Governance, Risk, and Compliance (GRC)
* Executives & Directors

---

## 🛠️ **Technologies Used**

* **Power BI Desktop**
* **Power Query M**
* **DAX**
* **Data Modeling**
* **GitHub Pages (HTML export)**

---

## 🤝 **Contributing**

If you’d like to enhance or extend the dashboard:

1. Fork the repository
2. Make your changes
3. Submit a pull request

---

## 📄 **License**

Choose a license (MIT, GPL, Proprietary).
If unsure, MIT is the easiest.

---

## ⭐ **Support the Project**

If this project was helpful, please give the repository a ⭐ on GitHub!


