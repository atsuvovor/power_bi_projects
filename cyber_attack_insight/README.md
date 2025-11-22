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

---


# ✅ **1. GitHub Project Description (Short About Section)**

> **Cyber Attack Insight Dashboard & Vulnerability Scorecard**
> A Power BI executive dashboard that analyzes cyber threats, vulnerability exposure, and system anomalies using a weighted scoring model and data-driven severity color mapping. The dashboard provides real-time insights into risk levels, attack patterns, operational impact, and key threat indicators (KTIs).
> Live Dashboard: [https://atsuvovor.github.io/power_bi_projects/cyber_attack_insight_dashboard.html](https://atsuvovor.github.io/power_bi_projects/cyber_attack_insight_dashboard.html)

---

# ✅ **3. Full Portfolio Case Study Page**

*(Use this as a GitHub Pages page, portfolio writeup, or PDF attachment)*

---

# **Cyber Attack Insight Dashboard & Vulnerability Scorecard**

**A Data-Driven Approach to Threat Detection, Severity Modeling & Operational Risk Intelligence**

---

## 📌 Project Overview

Cyberattacks continue to evolve in complexity, making it critical for organizations to monitor risk exposure, threat behavior, and system anomalies in real time. This project delivers a **Power BI executive dashboard** that transforms raw cybersecurity event data into **actionable intelligence**, powered by:

* A custom **weighted scoring model**
* Rich visual analytics
* Automated severity-based **color mapping**
* Dynamic slicing and drilldown capabilities
* Insightful threat correlations

The dashboard provides analysts, SOC teams, and leadership with a proactive early-warning system that highlights where risks are emerging and which areas require immediate intervention.

🔗 **View Live Dashboard**
[https://atsuvovor.github.io/power_bi_projects/cyber_attack_insight_dashboard.html](https://atsuvovor.github.io/power_bi_projects/cyber_attack_insight_dashboard.html)

---

## 🎯 Business Problem

Organizations often struggle with:

* Fragmented visibility across different security datasets
* Inconsistent severity scoring across tools
* Limited ability to detect patterns in activity logs
* Slow response times due to unclear risk priority

The goal was to build a **single pane of glass** that answers:

> *“What threats matter most right now, and why?”*

---

## 🧠 Solution Overview

This dashboard integrates **11 Key Threat Indicators**, normalizes them through a scoring engine, and applies a color-coded severity model to make high-risk conditions immediately visible.

### ✓ Key Deliverables

* **Vulnerability Scorecard**
* **Threat Severity Matrix**
* **Incident Timeline**
* **Attack Category Breakdown**
* **Login/File Access Anomaly Tracking**
* **CPU/Memory Usage Monitoring**

---

## 🧩 Scoring Engine (KTI Model)

The dashboard uses a **weighted scoring approach** to standardize different types of cybersecurity signals. Each KTI receives a numeric score ranging from 1–10 depending on its risk intensity.

These include:

* Severity
* Impact score
* Risk Level
* Response Time
* Unauthorized Access
* File Activity
* Login Attempts
* Network Data Transfer
* CPU/Memory anomalies

This scoring model ensures all threats are compared **on equal footing**.

---

## 🎨 Color Mapping Logic

**Risk visualization is powered by a Threat Level × Severity matrix**, producing a consistent and intuitive color system.

✔ Red tones → critical and high-risk
✔ Yellow tones → medium or elevated caution
✔ Green tones → low risk or normal conditions

Full mapping table (with color emoji bullets) is included in the README.

---

## 🕹️ Dashboard Experience

### Users can explore:

* **High-risk events** (via filters and scorecards)
* **Time of occurrence** (hour, day, trendline)
* **Attack categories**
* **Affected systems or activities**

### Interactions include:

* Cross-filtering
* Drilldowns
* Tooltip insights
* Custom slicers

The HTML export enables stakeholders to access the dashboard via the web without needing Power BI Desktop.

---

## 🧱 Architecture & Tools

| Layer         | Technology                           |
| ------------- | ------------------------------------ |
| Data Modeling | Power Query, DAX                     |
| Visualization | Power BI Desktop                     |
| Scoring Logic | Python-based model                   |
| Deployment    | GitHub Pages (HTML export)           |
| Documentation | GitHub README + Portfolio Case Study |

---

## 📈 What This Demonstrates

This project highlights capabilities in:

* Cybersecurity analytics
* Executive dashboard design
* Data modeling and normalization
* Severity and scoring logic engineering
* KPI frameworks
* UI/UX for risk visibility
* GitHub hosting for BI assets

---

## 📞 Contact

**Atsu Vovor**
Data & Analytics Consultant
📧 [atsu.vovor@bell.net](mailto:atsu.vovor@bell.net)  
🔗 LinkedIn: [](https://www.linkedin.com/in/atsu-vovor-mmai-9188326/)
📊 Portfolio: [](https://public.tableau.com/app/profile/atsu.vovor8645)

---

# **Cyber Attack Insight Dashboard & Vulnerability Scorecard**

*A Power BI Executive Dashboard for Threat Detection, Severity Scoring & Incident Response Intelligence*

🔗 **Live Dashboard:**
[https://atsuvovor.github.io/power_bi_projects/cyber_attack_insight_dashboard.html](https://atsuvovor.github.io/power_bi_projects/cyber_attack_insight_dashboard.html)

---

## 📌 **Overview**

The **Cyber Attack Insight Dashboard** provides a unified, interactive view of organizational threat activity, vulnerability scores, and operational risk signals. Designed for cybersecurity teams, analysts, and executive stakeholders, the dashboard transforms raw security event data into **actionable insights** by combining:

* Threat severity scoring
* Vulnerability classification
* Behavioral indicators
* System resource analytics
* Incident timelines
* Attack pattern correlations

This dashboard serves as a **proactive decision-support system** that highlights the most impactful cyber threats and operational risks in real-time.

---

## 🧩 **Key Features**

### 🔥 **1. Vulnerability Scorecard**

* Weighted scoring across **11 Key Threat Indicators (KTIs)**
* Executive-friendly visualization of **overall risk posture**
* Clear color semantics for intuitive interpretation

### 🛡️ **2. Threat Severity Classification**

* Automated mapping of severity to risk colors
* Supports quick scanning for urgent security events

### 📊 **3. Attack Pattern Insights**

* Behavioral anomalies
* Login attempt spikes
* Data transfer irregularities
* Resource usage anomalies (CPU, memory)

### 🕒 **4. Incident Timeline Visualization**

* Time-based attack progression
* Patterns across hours, days, categories

### 📁 **5. System Resource Monitoring**

* High-risk correlations between system load and attack behavior

---

## 📁 **Dataset & Variables**

The dashboard is built on a structured dataset containing key cybersecurity features, including:

| Field              | Description                                            |
| ------------------ | ------------------------------------------------------ |
| Severity           | Raw incident classification (Critical/High/Medium/Low) |
| Impact Score       | Normalized score representing operational impact       |
| Risk Level         | Threat actor classification                            |
| Response Time      | Time taken to respond to incidents                     |
| Category           | Attack type (Unauthorized Access, Phishing, etc.)      |
| Activity Type      | Behavioral indicators (login, data_transfer, etc.)     |
| Login Attempts     | Count of authentication attempts                       |
| Num Files Accessed | File activity monitoring                               |
| Data Transfer MB   | Outbound/inbound transfer volume                       |
| CPU Usage %        | Resource usage anomaly indicator                       |
| Memory Usage MB    | Memory consumption indicator                           |

---

# 🎯 **Key Threat Indicator (KTI) Scoring Model**

The Vulnerability Scorecard uses a **weighted scoring system** to normalize different cybersecurity signals.

| **KTI**            | **Condition Logic**                          | **Score Range** |
| ------------------ | -------------------------------------------- | --------------- |
| Severity           | Critical = 10, High = 8, Medium = 5, Low = 2 | 2–10            |
| Impact Score       | Input 1–10                                   | 1–10            |
| Risk Level         | High = 8, Medium = 5, Low = 2                | 2–8             |
| Response Time      | >7 days = 5, 3–7 days = 3, <3 days = 1       | 1–5             |
| Category           | Unauthorized Access = 8, Phishing = 6, etc.  | 1–8             |
| Activity Type      | High-risk types flagged                      | 1–5             |
| Login Attempts     | >5 = 5, 3–5 = 3, <3 = 1                      | 1–5             |
| Num Files Accessed | >10 = 5, 5–10 = 3, <5 = 1                    | 1–5             |
| Data Transfer MB   | >100 = 5, 50–100 = 3, <50 = 1                | 1–5             |
| CPU Usage %        | >80% = 5, 60–80 = 3, <60 = 1                 | 1–5             |
| Memory Usage MB    | >8000 = 5, 4000–8000 = 3, <4000 = 1          | 1–5             |

---

# 🎨 **Color Mapping Logic (Threat Level × Severity)**

This is the complete color logic used in the Power BI scoring visuals.

### **Threat Severity → Color Mapping Table (With Emoji Bullets)**

| **Threat Level** | **Severity** | **Color Used**       |
| ---------------- | ------------ | -------------------- |
| **Critical**     | Critical     | 🔴 **Dark Red**      |
| Critical         | High         | 🟥 **Red**           |
| Critical         | Medium       | 🟧 **Orange-Red**    |
| Critical         | Low          | 🟠 **Orange**        |
| **High**         | Critical     | 🟥 **Red**           |
| High             | High         | 🟧 **Orange-Red**    |
| High             | Medium       | 🟠 **Orange**        |
| High             | Low          | 🟨 **Yellow-Orange** |
| **Medium**       | Critical     | 🟠 **Orange**        |
| Medium           | High         | 🟨 **Yellow-Orange** |
| Medium           | Medium       | 🟨 **Yellow**        |
| Medium           | Low          | 💛 **Light Yellow**  |
| **Low**          | Critical     | 🟨 **Yellow**        |
| Low              | High         | 💛 **Light Yellow**  |
| Low              | Medium       | 💚 **Green-Yellow**  |
| Low              | Low          | 🟩 **Green**         |

---

### 🧠 **Behind-the-Scenes Python Logic**

```python
def assign_color(threat, severity):

    if threat == "Critical":
        if severity == "Critical":
            return "Dark Red"
        elif severity == "High":
            return "Red"
        elif severity == "Medium":
            return "Orange-Red"
        else:
            return "Orange"

    elif threat == "High":
        if severity == "Critical":
            return "Red"
        elif severity == "High":
            return "Orange-Red"
        elif severity == "Medium":
            return "Orange"
        else:
            return "Yellow-Orange"

    elif threat == "Medium":
        if severity == "Critical":
            return "Orange"
        elif severity == "High":
            return "Yellow-Orange"
        elif severity == "Medium":
            return "Yellow"
        else:
            return "Light Yellow"

    else:  # Low threat
        if severity == "Critical":
            return "Yellow"
        elif severity == "High":
            return "Light Yellow"
        elif severity == "Medium":
            return "Green-Yellow"
        else:
            return "Green"
```

---

# 🚀 **How to Use the Dashboard**

### **1. Open the Online Dashboard**

Click on:
➡️ [https://atsuvovor.github.io/power_bi_projects/cyber_attack_insight_dashboard.html](https://atsuvovor.github.io/power_bi_projects/cyber_attack_insight_dashboard.html)

### **2. Explore Key Tabs**

* **Overview Page** — overall risk score, severity heatmaps
* **Threat Patterns** — detects anomalies and spikes
* **System Metrics** — resource indicators tied to risk
* **Vulnerability Scorecard** — weighted scoring of KTIs

### **3. Drill into High-Risk Areas**

Use slicers such as:

* Date range
* Attack category
* Severity level
* Activity type

### **4. Export Insights**

* Power BI allows exporting tables and charts for reports
* Screenshots from the HTML dashboard can be used in presentations

---

# 🧱 **Technical Architecture**

| Component           | Technology                            |
| ------------------- | ------------------------------------- |
| Data Processing     | Power Query, DAX                      |
| Visualization       | Microsoft Power BI Desktop            |
| Hosting             | GitHub Pages (HTML Export)            |
| Logic/Documentation | Python-based scoring model (external) |
| File Export         | `.pbix` + HTML rendering              |

---

---

## 🧱 Architecture & Tools

| Layer         | Technology                           |
| ------------- | ------------------------------------ |
| Data Modeling | Power Query, DAX                     |
| Visualization | Power BI Desktop                     |
| Scoring Logic | Python-based model                   |
| Deployment    | GitHub Pages (HTML export)           |
| Documentation | GitHub README + Portfolio Case Study |

---

## 📈 What This Demonstrates

This project highlights capabilities in:

* Cybersecurity analytics
* Executive dashboard design
* Data modeling and normalization
* Severity and scoring logic engineering
* KPI frameworks
* UI/UX for risk visibility
* GitHub hosting for BI assets

---

# 🔒 **Security Disclaimer**

This dashboard represents **synthetic** or **anonymized** data for demonstration purposes.
It does not expose real organizational threat data.

---

# 🙌 **Credits**

Created by **Atsu Vovor**
📧 [atsu.vovor@bell.net](mailto:atsu.vovor@bell.net)
🔗 LinkedIn: [https://www.linkedin.com/in/atsu-vovor-mmai-9188326/](https://www.linkedin.com/in/atsu-vovor-mmai-9188326/)
📊 Tableau Portfolio: [https://public.tableau.com/app/profile/atsu.vovor8645](https://public.tableau.com/app/profile/atsu.vovor8645)






