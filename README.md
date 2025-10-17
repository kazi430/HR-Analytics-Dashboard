##HR Analytics Dashboard – Power BI Project


1️⃣ Project Overview

The HR Analytics Dashboard is designed to help HR professionals and management teams analyze workforce demographics, monitor attrition trends, and understand employee distribution across departments, age bands, and other key dimensions.
The goal of this dashboard is to provide data-driven insights for reducing attrition, improving workforce planning, and ensuring diversity and inclusion within the organization.

2️⃣ Business Objectives

Monitor employee headcount across departments and demographics.

Track attrition trends (voluntary vs. involuntary) over time.

Analyze salary distribution and average compensation.

Understand diversity metrics (gender, race, citizenship, marital status).

Provide a detailed employee view for quick HR decision-making.

3️⃣ Data Sources & Structure
Table Name	Description	Key Columns
Employees	Contains core employee data (personal, job, and demographic info)	EmpID, Name, DOB, Sex, Department, Position, Salary
Attrition	Tracks terminated employees, reasons, and dates	EmpID, Termination Date, Reason, Type (Voluntary/Involuntary)
Departments	Department-level mapping	DeptID, Department Name, Manager
Calendar	Date dimension for time-based trends	Date, Month, Year, Quarter
4️⃣ Data Cleaning & Transformation (Power Query)

Removed duplicate and null entries.

Created a custom date table using DAX for time intelligence.

Converted date fields into proper Date data type.

Created calculated columns:

Age = DATEDIFF(DOB, TODAY(), YEAR)

Employee Age Band (e.g., 20–29, 30–39, etc.)

Tenure = DATEDIFF(DateOfHire, TODAY(), YEAR)

Merged Attrition table with Employee details for unified reporting.

5️⃣ Data Modeling (Star Schema)

Central Table: Employees

Dimension Tables: Departments, Calendar, Attrition

Relationships:

Employees[EmpID] → Attrition[EmpID]

Employees[DateOfHire] → Calendar[Date]

Employees[DeptID] → Departments[DeptID]

6️⃣ Key DAX Measures
Measure Name	Formula	Description
Total Employees	COUNT(Employees[EmpID])	Total active workforce
Total Terminated	COUNT(Attrition[EmpID])	Number of employees who left
Attrition Rate %	DIVIDE([Total Terminated],[Total Employees]+[Total Terminated])	Percentage of employees who left
Average Salary	AVERAGE(Employees[Salary])	Avg salary per employee
Active Employees	CALCULATE(COUNT(Employees[EmpID]), FILTER(Employees, Employees[Status]="Active"))	Count of active employees
Terminated by Reason	COUNTROWS(FILTER(Attrition, Attrition[Reason] = "Specific"))	Termination reason count
Attrition by Department	CALCULATE([Attrition Rate %], ALLEXCEPT(Employees, Employees[Department]))	Department-wise attrition
7️⃣ Dashboard Structure
📍 Page 1: Overview

Purpose: Provide a summary of workforce demographics and structure.
Visuals Used:

KPI Cards → Total Employees, Avg Salary, Attrition Rate

Donut Charts → Employees by Sex, Citizenship, Marital Status

Bar Charts → Employees by Department, Race, Age Band

Line Chart → Monthly Employee Growth Trend

Insights:

Total Employees: 311

Average Salary: $69K

Attrition Rate: 50%

Male to Female ratio: 57% : 43%

Majority of employees (95%) are US Citizens

Most employees are aged 40–49, primarily in the Production department.

📍 Page 2: Attrition

Purpose: Analyze employee attrition and termination patterns.
Visuals Used:

KPI Cards → Terminated Employees, Active Employees, Attrition Rate

Donut Chart → Terminated by Sex

Line Chart → Attrition Rate Over Time

Bar Chart → Termination Reasons (e.g., career change, relocation, performance, etc.)

Insights:

Total Terminated Employees: 104

Top termination reasons: “Another Position” and “Unhappy”

Attrition Rate increased to 50%, showing spikes in specific years (2015–2017).

Higher attrition among male employees (≈58%).

📍 Page 3: Employee Details

Purpose: Provide detailed employee-level insights with dynamic filters.
Visuals Used:

Interactive Table with slicers: Department, Position, Year

Columns: Employee ID, Name, Gender, DOB, Citizenship, Department, Hire Date, Age Band, Status

Designed for drill-through and individual analysis.

8️⃣ Key Insights Summary

✅ High attrition (50%) in the Production and IT/IS departments.
✅ Average employee age is around 45 years, indicating an experienced workforce.
✅ Employee gender ratio is relatively balanced, ensuring diversity.
✅ Major terminations due to career change or better opportunities.
✅ Average salary stable around $69K across departments.

9️⃣ Recommendations

Conduct employee satisfaction surveys to identify causes of unhappiness.

Implement career development programs to reduce voluntary attrition.

Monitor department-wise attrition trends monthly.

Maintain competitive pay structure in high-turnover roles.

Introduce mentorship initiatives for mid-career employees (30–39 age band).

🔟 Tools & Techniques Used

Power BI Desktop (2024)

Power Query (ETL) for data cleaning and shaping

DAX for calculations & KPIs

Data Modeling (Star Schema)

Interactive Visuals – KPI Cards, Donut Charts, Bar & Line Charts, Tables

11️⃣ Conclusion

The HR Analytics Dashboard enables HR teams to visualize workforce composition, analyze attrition causes, and optimize employee retention strategies.
By leveraging Power BI’s interactive capabilities, this dashboard transforms raw HR data into clear, actionable insights that support evidence-based decision-making.

12️⃣ Developer Information

Developer: Kazi Abubakar
Project Type: HR Analytics Dashboard (Power BI)
Version: 1.0 (October 2025)
Dataset Size: 311 Employees
Refresh Type: Manual Import Mode
Tools Used: Power BI Desktop, Excel
