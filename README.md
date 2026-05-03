PV Productivity & Performance Analysis Dashboard

A Power BI dashboard built to give pharmacovigilance operations teams real-time visibility into case processing performance, SLA compliance, and associate-level productivity - replacing hours of manual reporting with a single source of truth.


The Problem It Solves
In pharmacovigilance (PV) operations, case processing teams handle thousands of drug safety cases daily across multiple workflows: Data Entry, QC, QC Review, Medical Review, Data Entry Review, and Distribution Closure. Before this dashboard existed, managers faced three core blind spots:
1. No hourly visibility into associate output
Productivity was reviewed at end-of-day or week. If an associate fell behind during the 11-13 hour slot, nobody knew until it was too late to course-correct.
2. SLA breaches were discovered after the fact
Cases that breached the 24/48-hour SLA window were only identified during manual audits. There was no early-warning system tied to case type, team, or workflow.
3. Processing time analysis required hours of manual work
Calculating average turnaround time per team, workflow, or associate meant pulling raw exports into Excel and building pivot tables - a process repeated weekly.
This dashboard eliminates all three problems.

Dashboard Pages
Page 1- Executive Overview
Audience: Operations managers, leadership
Key metrics: Total cases (60,351), MTD volume, overall SLA%, average processing time
Visuals:

Monthly trend showing total cases + avg case cycle time (dual-axis)
Donut chart: total cases by team (Spontaneous 42.3%, Clinical Trial 29.5%, Literature 16.2%, E2B 12.1%)
Delay share by team (horizontal bar)- Spontaneous leads at 46.06%
SLA breach rate by workflow (Data Entry 39.9%, QC 34.8%, QC Reviewed 29.2%)


Page 2- Team Daily Performance
Audience: Team leads, shift supervisors
Key metrics: Cases today (95), Avg DE/Hr (59.85%), Daily target hit% (75%), Below-target count (4)
Visuals:

Hourly productivity heatmap: associates (rows) × hour slots 09–18 (columns) with case counts -pink = low, teal = high
Target % bar chart by associate (Top 5 / Bottom 5 toggle)
Associate workflow breakdown table: Completed, Pending, Breached counts per workflow


Page 3- Processing Time Drilldown
Audience: Operations analysts, process improvement teams
Key metrics: Avg DE Time (58.17 min), Avg QC Time (27.87 min), Avg Medical Review Time (149.59 min), Total End-to-End Time (158.44 min)
Visuals:

Sankey-style decomposition: End-to-End Time → by Team → by Workflow → by Associate
SLA Breach Heatmap (Team × Workflow matrix with conditional formatting)
Avg Queue Minutes by workflow (Medical Review highest at 19.4 min)


Page 4- Raw Case Data Table
Audience: Data analysts, compliance teams
Columns: case_id, day_name, hour_slot, is_sla_breached, queue_start, turnaround_minutes, role, delay_minutes, is_working_day
Use case: Drill-through from any visual to inspect individual case records; exportable for audit trails

Key Features
FeatureDescriptionHourly heatmapPer-associate productivity grid broken into 1-hour slots; color-coded for instant pattern recognitionSLA breach heatmapTeam × Workflow matrix showing breach % — highlights worst-performing combinationsProcessing time SankeyEnd-to-end flow decomposed from team → workflow → associate levelDelay attributionWhich teams and workflows contribute most to case delaysCase type filterToggle between Clinical Trial, E2B, Literature, Spontaneous across all pagesDate range slicerFull year 2025 coverage with daily granularityTop 5 / Bottom 5 toggleInstantly switch between highest and lowest performers in target % view

Data Model
The dashboard is built on a star schema optimized for time intelligence and workflow analysis:
fact_cases
├ dim_date          (calendar table with working day flags)
├dim_associate     (name, team, role)
├ dim_workflow      (workflow_name, sla_threshold_minutes)
└ dim_case_type     (Clinical Trial / E2B / Literature / Spontaneous)
Key DAX measures include:

SLA Breach % = DIVIDE(COUNTROWS(FILTER(fact_cases, fact_cases[is_sla_breached] = TRUE())), COUNTROWS(fact_cases))
Avg DE/Hr - calculated using time intelligence over working-day-only calendar
Delay Minutes - difference between actual turnaround and SLA threshold
Target Hit % - associate-level daily target attainment rate


Tech Stack

Power BI Desktop - report authoring and publishing
DAX - all KPI measures, time intelligence, conditional formatting logic
Power Query (M) - data transformation, working day classification, hour slot extraction
Star Schema - fact + dimension model for clean, performant aggregations
Row-Level Security (RLS) - team leads see only their team's data


Screenshots
PagePreviewExecutive Overviewscreenshots/pg1_overview.pngTeam Daily Performancescreenshots/pg2_daily.pngProcessing Time Drilldownscreenshots/pg3_processing.pngRaw Case Datascreenshots/pg4_data.png

Business Impact

Reduced manual reporting time from ~4 hours/week to zero - all metrics update automatically on data refresh
Enabled same-day SLA intervention - team leads now catch breaching cases within the hour, not the next morning
Identified Spontaneous team as highest delay source (46% of all delays) - led to targeted process review
Medical Review flagged as queue bottleneck - avg queue time 19.4 minutes vs 5.5 minutes for all other workflows


How to Use This Report

Clone or download the .pbix file from this repository
Open in Power BI Desktop (free download from Microsoft)
Replace the data source connection with your own case management export (CSV/SQL)
Publish to Power BI Service for shared team access


Note: The sample dataset covers 01-Jan-2025 to 31-Dec-2025 with anonymized case IDs. All associate names in the demo are fictional.


About the Author
Built by a PV operations analyst with hands-on experience in pharmacovigilance case processing workflows. This dashboard was designed with direct input from team leads and associates who needed actionable daily intelligence, not just historical reports.
Open to: Data analyst / BI developer roles in pharma, healthcare operations, or regulated industries.

License
MIT License — free to use, adapt, and build on with attribution.
