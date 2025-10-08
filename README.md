# IT Ticket Support Analysis Dashboard

[![View Portfolio](https://img.shields.io/badge/View%20Portfolio-%23000000.svg?style=for-the-badge&logo=firefox&logoColor=#FF7139)](https://www.datascienceportfol.io/mohan_Srinivas/projects/4)
[![View Dashboard](https://img.shields.io/badge/View%20Dashboard-%23000000.svg?style=for-the-badge&logo=Codeforces&logoColor=gold)](https://app.powerbi.com/view?r=eyJrIjoiMDYyZGU5OWItZjliMC00NjE5LWFhMmEtMGI1OGZkMDE4NTJhIiwidCI6IjQ2NTRiNmYxLTBlNDctNDU3OS1hOGExLTAyZmU5ZDk0M2M3YiIsImMiOjl9)

## Table of Contents
  - [Problem Statement](#problem-statement)
  - [Project Planning using Star Method](#project-planning-using-star-method)
  - [Data Source](#data-source)
  - [Data Preprocessing \& ETL](#data-preprocessing--etl)
  - [Data Modelling](#data-modelling)
  - [Data Analysis](#data-analysis)
  - [Dashboard](#dashboard)
  - [Findings](#findings)
  - [Tools And Softwares](#tools-and-softwares)


## Problem Statement
<details>
<summary>
$\textsf{\color{blue}{View Problem Statement ➡️}}$
</summary><br>

**Problem**

Organizations often face difficulties in monitoring IT support tickets. Without insights into ticket categories, resolution efficiency, and geographic patterns, support teams struggle with long resolution times, workload imbalances, and lack of automation.

This project aims to deliver a comprehensive Power BI dashboard powered by ZoomCharts visuals to analyze:

- Ticket distribution across queues & tags

- Resolution times & SLA adherence

- Location-based ticket volumes & delays

- Automation opportunities for process improvements

**Challenges:**

- Which types of injuries occur most frequently?
- Which sports or events have the highest rate of injury?
- Are injuries more common in specific athlete age groups or genders?
- How does injury severity vary across different types of sports or positions?
- How long does recovery typically take for various injury types?
- Which treatment methods are most effective for speeding up recovery?
- Do certain coaches or teams have consistently lower injury rates?
- Are there regional differences in injury frequency or severity?
- Does the playing surface or competition level affect injury occurrence?

**Key Questions to Explore**

- Ticket Types & Tags

  - What kinds of issues (bugs, requests, features) come up most often?

  - Which support teams or queues handle the most tickets?

  - How are different tags (like "Security", "Integration", or "Documentation") used?

- Resolution Time & Priorities

  - How long does it take to resolve tickets, on average?

  - Do higher-priority tickets get resolved faster?

  - Which types of tickets take the longest to close?

- Locations & Volume

  - Which countries or regions submit the most tickets?

  - Are there certain locations that see more delays or specific issues?

- Process Improvement

  - Can we group similar tickets to create automated replies or help articles?

  - Are the agent responses helpful and aligned with what the user asked?

  - Where can the support team save time or improve service quality?

- Resolution Time & Priorities

  - How does resolution time vary across tags and priorities?

  - Which countries face more SLA breaches?

  - Do secondary tags highlight hidden workload categories?

</details>


## Project Planning using Star Method
<details>
<summary>
$\textsf{\color{blue}{View Stratergy ➡️}}$
</summary><br>

### 📝 S - Situation

Support leadership lacked a 360° view of ticket operations—they couldn’t easily see ticket types, resolution times, or regional volumes. High-priority workloads and automation opportunities were invisible.

**Key Questions Driving the Situation:**

- What kinds of issues (bugs, requests, features) come up most often?
- Which support teams/queues handle the most tickets?
- Which countries or regions submit the most tickets?
- Are there locations with recurring delays or unique issue types?
- This situation highlights the need for a systematic data model, reliable KPIs, and trend analysis to guide support operations.

### 🎯 T - Task

The objective was to design and implement a centralized analytics solution that:

- Consolidates raw data from injury logs, treatments, costs, and player details.

- Provides multi-dimensional insights at player, regional, and organizational levels.

- Enables stakeholders (doctors, trainers, coaches, executives) to explore:

    - Most frequent injury types and affected body parts.

    - Recovery timelines by severity, treatment, and sport.

    - Cost trends (MOM, YOY) across treatments and surfaces.

    - Coach and team effectiveness in reducing recovery times.

    - Regional and demographic (age, gender) variations.

### ⚡ A - Action

- Imported raw data from Excel (IT_Support_Ticket_Desk.xlsx).

- Built custom Calendar table to enable time intelligence (YOY/MOM).

- Applied Power Query ETL:

  - Extracted Month, Week, Day, Weekend flags.
  - Created Resolution Time column (Date difference).
  - Derived WeekNum (1–5) based on ticket date.
  - Added Automation flag based on keywords in tags & answers.
- Designed Data Model (Fact Tickets + Calendar + Measures + Data     Dictionary).
- Built KPIs & Measures: Total Tickets, Avg Resolution Time, High-Priority %, YOY/MOM comparisons.
- Created interactive visuals using ZoomCharts for drilldowns.

- Built Resolution Deep Dive dashboard analyzing Avg Resolution Time by priority & tags.

- Mapped SLA breaches geographically to highlight country-level inefficiencies.

- Added drilldowns into secondary tags for hidden workload classification.

### 🏆 R - Result

- Delivered a dynamic Power BI dashboard with real-time filtering by tags, country, and priority.

- Improved visibility into department workload (Technical Support = highest tickets).

- Highlighted automation opportunities to reduce manual work by 28.7% (weekend load).

- Empowered managers to monitor resolution efficiency and optimize staffing.

- Better customer experience from fewer SLA breaches and quicker handling of high-priority tickets.

- Strategic reporting enabling leadership to track progress and make data-driven improvements.

- Identified tags (like Documentation & Security) as slowest to resolve.

- Mapped SLA breaches showing Belgium & France with highest delays.

- Secondary tags revealed hidden trends (e.g., repetitive “Integration” issues), supporting automation strategy.

</details>


## Data Source
<details>
<summary>
$\textsf{\color{blue}{View Data Source ➡️}}$
</summary><br>

- **Dataset:** Data Set Provided By [ZoomCharts](https://zoomcharts.com/en/microsoft-power-bi-custom-visuals/challenges/fp20-analytics-july-2025)

- File: IT_Support_Ticket_Desk.xlsx.

- Contains ticket-level records with attributes such as:

- Ticket ID, Date, Resolution Date

- Subject, Answer, Tags (Primary, Secondary, Technical, Category, etc.)

- Priority (High/Medium/Low)

- Queue (Department)

- Country (with lat-long coordinates)data.

</details>


## Data Preprocessing & ETL

<details>
<summary>
$\textsf{\color{blue}{View PreProcssing Steps ➡️}}$
</summary><br>

The raw dataset was extracted from IT_Support_Ticket_Desk.xlsx and processed in Power Query (M) to prepare it for analysis in Power BI.

**Steps Performed**

**1. Data Ingestion**

- Loaded Excel sheet “Data” from the source file.

- Promoted headers and applied appropriate data types for all columns (e.g., Ticket ID → Int64, Date → Date, Latitude/Longitude → Decimal).

**2. Date Enrichment**

Created multiple time-based attributes to enable trend analysis:

- Month → Extracted month name from Date.

- Date(DD) → Extracted day number.

- Day → Extracted weekday name.

- WeekNum → Custom logic assigning each ticket to Week 1–5 within a month.

- Resolution Month → Extracted month name from Resolution Date.

These features power time-series analysis, SLA compliance by weekdays, and YOY comparisons.

**3. Ticket Processing Features**

- Resolution Time (Days) → Calculated as Resolution Date – Date for ticket turnaround tracking.

- Automation Flag → Added logic to detect tickets that could be automated.

   Criteria: presence of words like “Documentation”, “resolved”, “automatically”, “fix”, “restarted”.

   Output standardized as ✔️ Yes (eligible for automation) or ❌ No.

- Answer Normalization → Replaced null values in Answer column with "No Answer".

**4. Data Cleaning**

- Replaced error values in Automation with default ❌ No.

- Ensured consistent naming of new columns (e.g., Resolution Month, Date(DD)).

**5. Final Result**

The cleaned dataset now includes both original ticket attributes (Type, Queue, Priority, Tags, Location) and engineered features (Resolution Time, SLA Weeks, Automation flag, enriched Date dimensions).

This ensures the dataset is ready for star schema modeling, where:

- Fact Table → Ticket transactions with measures like Resolution Time, SLA compliance.

- Dimension Tables → Calendar, Location, Queue/Team, Tags, Priority

✅ This ETL pipeline transforms raw support desk data into a rich analytical dataset, enabling insights into:

- Ticket volumes by time, location, and type.

- SLA compliance and resolution efficiency.

- Automation opportunities for repetitive issues

</details>

## Data Modelling
<details>
<summary>
$\textsf{\color{blue}{View Modelling ➡️}}$
</summary> <br>

<img width="700" height="400" alt="Image" src="https://github.com/user-attachments/assets/8b5600b7-bfca-48f0-b1ca-e40a9fb4fede" />

**Fact Table**

- Tickets (TicketID, Date, Resolution Date, Queue, Priority, Tags, Country, Automation, Resolution Time).

**Relationships**

- Tickets[Date] → Calendar[Date] (Many-to-One).

- Supporting measures defined in _Measures.

**Dimension Tables**

- Calendar (Date, Month, Quarter, Week, Year, Weekend Flag).

- Data Dictionary (Business Glossary).

- Measures (KPIs).

</details>


## Data Analysis
<details>
<summary>
$\textsf{\color{blue}{Power BI: View Created Dax Measures, Columns, Tables ➡️}}$
</summary><br>

**Measures:**
**📊 IT Support Ticket Analysis**

**Tickets & SLA**
```
1. Total Tickets =
COUNTROWS(FactTickets)

2. Open Tickets =
CALCULATE(COUNTROWS(FactTickets), FactTickets[Status] = "Open")

3. Closed Tickets =
CALCULATE(COUNTROWS(FactTickets), FactTickets[Status] = "Closed")

4. Within SLA =
CALCULATE(COUNTROWS(FactTickets), FactTickets[WithinSLA] = "Yes")

5. Outside SLA =
CALCULATE(COUNTROWS(FactTickets), FactTickets[WithinSLA] = "No")
```

**®️Resolution & Priorities**

1. Treatment & Player Outcomes

```
1. Avg Resolution Time (Days) =
AVERAGE(FactTickets[ResolutionTimeDays])

2. Avg Resolution Time YTD =
CALCULATE(
    [Avg Resolution Time (Days)],
    DATESYTD(DimDate[Date])
)

3. PY Avg Resolution Time YTD =
CALCULATE(
    [Avg Resolution Time (Days)],
    DATESYTD(SAMEPERIODLASTYEAR(DimDate[Date]))
)

4. Avg Res Time YOY % =
DIVIDE(
    [Avg Resolution Time YTD] - [PY Avg Resolution Time YTD],
    [PY Avg Resolution Time YTD]
)

5. Avg Res Time Trend Text =
SWITCH(
    TRUE(),
    [Avg Res Time YOY %] > 0, "↑ Slower",
    [Avg Res Time YOY %] < 0, "↓ Faster",
    "→ Stable"
)

6. Total High Priority Tickets =
CALCULATE(COUNTROWS(FactTickets), FactTickets[Priority] = "High")

7. % High Priority Tickets =
DIVIDE([Total High Priority Tickets], [Total Tickets])

8. High Priority Tickets YTD =
CALCULATE(
    [Total High Priority Tickets],
    DATESYTD(DimDate[Date])
)

9. PY High Priority Tickets YTD =
CALCULATE(
    [Total High Priority Tickets],
    DATESYTD(SAMEPERIODLASTYEAR(DimDate[Date]))
)

10. YOY High Priority % =
DIVIDE(
    [High Priority Tickets YTD] - [PY High Priority Tickets YTD],
    [PY High Priority Tickets YTD]
)

11. High Priority Trend Text =
SWITCH(
    TRUE(),
    [YOY High Priority %] > 0, "↑ Increasing",
    [YOY High Priority %] < 0, "↓ Decreasing",
    "→ Stable"
)

12. Avg Resolution Time by Tag =
CALCULATE(
    AVERAGE(FactTickets[ResolutionTimeDays]),
    VALUES(FactTickets[Tag])
)

13. Avg Resolution Time by Priority =
CALCULATE(
    AVERAGE(FactTickets[ResolutionTimeDays]),
    VALUES(FactTickets[Priority])
)

14. SLA Breach % =
DIVIDE([Outside SLA], [Total Tickets])

15. SLA Breaches by Country =
CALCULATE(
    [Outside SLA],
    VALUES(FactTickets[Country])
)

16. Tickets by Secondary Tag =
COUNTROWS(FactTickets)
```

**📈Growth & Trends**


```
1. Total Tickets YTD =
CALCULATE([Total Tickets], DATESYTD(DimDate[Date]))

2. PY Total Tickets YTD =
CALCULATE([Total Tickets], DATESYTD(SAMEPERIODLASTYEAR(DimDate[Date])))

3. YOY Growth (%) =
DIVIDE(
    [Total Tickets YTD] - [PY Total Tickets YTD],
    [PY Total Tickets YTD]
)

4. YOY Growth =
[Total Tickets YTD] - [PY Total Tickets YTD]
```
**🌍Volume & Location**

```
1. TicketsByLocation =
COUNTROWS(FactTickets)   // Put Location column in visual for breakdown

2. Avg Tickets Raised Per Day =
AVERAGEX(
    VALUES(DimDate[Date]),
    CALCULATE([Total Tickets])
)

3. Avg Tickets Resolved Per Day =
AVERAGEX(
    VALUES(DimDate[Date]),
    CALCULATE([Closed Tickets])
)
```


</details>

## Dashboard
<details>
<summary>
$\textsf{\color{blue}{View Images ➡️}}$
</summary> <br>


> ### 1. Executive Summary 

- Total Tickets (overall volume)
- Tickets Raised vs Resolved (trend over time)
- Ticket Distribution by Type (Incidents, Requests, Bugs, Features)
- SLA Compliance (Within SLA vs Outside SLA %)
- Priority Breakdown (High / Medium / Low)
- YOY Growth % of Tickets (Raised vs Previous Year)
- Country-Level Ticket Volumes (Top 5 countries / Map view)
- Queue-wise Ticket Workload (which support teams handle most)

> <a href="https://app.powerbi.com/view?r=eyJrIjoiNWU0MmMyNGQtODFiMS00NzI3LTk1MDMtYWU3OTNlNmE1MjM4IiwidCI6IjQ2NTRiNmYxLTBlNDctNDU3OS1hOGExLTAyZmU5ZDk0M2M3YiIsImMiOjl9" target="_blank"><img width="700" height="450" alt="Image" src="https://github.com/user-attachments/assets/daf7b7ae-3d56-424f-a516-0f0a195d015c" />
</a>

> ### 2.Resolution Deep Dive 

- Avg Resolution Time by Priority & Tag
- SLA Performance (Inside SLA vs Outside SLA)
- SLA Breach Map by Country
- Secondary Tag Drilldowns

> <img width="700" height="450" alt="Image" src="https://github.com/user-attachments/assets/6eaebfca-86ae-4285-b3bc-940d99e9878c" />

</details>


## Findings
<details>
<summary>
$\textsf{\color{blue}{View Findings ➡️}}$
</summary><br>

Ticket Distribution

- Total Tickets: 11,923 (↓ 58.8% vs PY).

- Technical Support = highest workload (3,412).

- Belgium reported most tickets.

Priority Trends

- High-priority tickets = 4,571 (↓ 59.8% vs PY).

- Medium priority dominated (41.5%).

Resolution Insights

- Avg Resolution Time = 2.82 days (↑ 0.6% vs PY).

- Weekdays = 71.3% workload vs 28.7% on weekends.

Automation Opportunities

- Tags & Answers identified automation-ready tickets.

- Potential to reduce manual work in documentation, sync issues, and feedback loops.

Resolution Deep Dive Insights

- Avg Resolution Time = 2.82 days; but Documentation & Security tags took longest.

- High-priority tickets not always faster — many still breach SLA.

- Belgium & France show highest SLA breach rates.

- Secondary tags highlight repetitive Integration & Access issues, suitable for automation.

</details>


## Tools And Softwares
<details>
<summary>
$\textsf{\color{blue}{View Tools ➡️}}$
</summary><br>
  
- **Power BI** → data modeling & dashboard development
- **DAX** → Custom KPIs & calculated measures
- **Excel/CSV** → Raw dataset handling
- **Icons/Images** → For visual representation in dashboard
- **ZoomCharts** →(Advanced visuals for drilldowns & maps)
- 
</details>
