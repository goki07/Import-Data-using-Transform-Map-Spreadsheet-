Import Data Using Transform Maps
📌 Project Overview
This micro project demonstrates how to import structured employee data from an external spreadsheet into the ServiceNow platform using Import Sets and Transform Maps.
The project simulates a real-world scenario where bulk employee data is received in Excel format and migrated into ServiceNow efficiently and accurately.
🔄 Project Flow
```text
Excel / Google Spreadsheet
          │
          ▼
     Load Data
          │
          ▼
   Import Set Table
          │
          ▼
     Transform Map
          │
          ▼
      Coalesce
          │
          ▼
   Employee Test Table
          │
          ├──────────► Reports
          │
          └──────────► Dashboard
```
The spreadsheet data is first loaded into an Import Set table, which acts as a staging area. A Transform Map then maps source fields to the appropriate target-table fields. After transformation, records are created or updated in the target table and validated.
---
🎯 Objectives
Import employee data from an Excel spreadsheet into ServiceNow.
Create a custom employee target table.
Create and configure an Import Set table.
Create a Transform Map between source and target tables.
Map source fields to target fields.
Use Coalesce to prevent duplicate records.
Validate inserted and updated records.
Create reports based on employee data.
Create a dashboard containing the reports.
---
🛠️ ServiceNow Components Used
Import Sets
Transform Maps
Custom Tables
Field Maps
Coalesce
Reports
Dashboards
List/Form Layout
Excel / Spreadsheet data
---
🚀 Step-by-Step Implementation
Phase 1: Prepare the Spreadsheet
Open a new Google Spreadsheet.
Create sample employee data.
Download the spreadsheet in `.xlsx` format.
Example filename:
```text
Sample Spreadsheet.xlsx
```
The spreadsheet acts as the external source for the employee data.
---
Phase 2: Create the Custom Employee Table
Navigation
```text
Tables → Create New
```
Table Details
Property	Value
Label	Employee Test
Name	u_employee_test
After creating and saving the table:
Scroll to the bottom of the table form.
Click Show Form.
Open the Form Context Menu / Additional Actions.
Select:
```text
Configure → Form Layout
```
Click New to create fields.
Required Fields
Field	Type
Employee ID	String
Employee Name	String
Email	String
Department	String
Location	String
Click Add after creating each field.
Save the form.
Verify that all fields are displayed on the Employee Test form.
---
Phase 3: Create the Import Set Table
Navigation
```text
Application Navigator → Load Data
```
Create an Import Set table.
Import Set Details
Property	Value
Label	Employee Import
Name	u_employee_import
The name is automatically populated.
Click Submit.
After submission, use the Create Transform Map option.
---
Phase 4: Create the Transform Map
Create the Transform Map from the Import Set.
Transform Map Details
Property	Value
Name	Sample Spreadsheet Import
Source Table	Employee Import
Target Table	Employee Test
Field Mapping
Click Auto Map Matching fields where applicable.
Use Mapping Assist to map the source fields to the target fields.
Verify the Source and Target field mappings.
Click Save.
Transformation
Click:
```text
Transform → Transform
```
After transformation, verify that the process displays a successful status.
---
Phase 5: Transform Data & Validate
Navigation
Open the Employee Test table from the Application Navigator.
After a successful import:
```text
Import Set
     │
     ▼
Transform Map
     │
     ▼
Employee Test Table
```
The imported employee records should now be available in the Employee Test table.
You can rearrange the displayed fields using Personalized List Columns.
Final Result
The employee records are successfully imported into ServiceNow using the Import Set and Transform Map.
---
Phase 6: Enable Coalesce to Avoid Duplicate Records
What is Coalesce?
Coalesce is used in the Transform Map to identify existing records during imports.
In this project, Coalesce is used so that existing employee records can be updated instead of creating duplicate records.
Steps
Open the Transform Map under the relevant application menu.
Open:
```text
Sample Spreadsheet Import
```
Go to the Field Maps related list.
Select an appropriate field.
Change its Coalesce value from:
```text
False → True
```
Save the Transform Map.
Import the Excel data again.
Coalesce Flow
```text
New Excel Record
       │
       ▼
Compare Coalesce Field
       │
       ├── Existing Record ──► Update
       │
       └── New Record ───────► Insert
```
This prevents duplicate employee records when the same employee data is imported again.
---
Phase 7: Insert New Data in Excel Format
To test Coalesce and record updates:
Navigation
```text
All → Load Data
```
Open Load Data under the Import Set area.
Configuration
Property	Value
Import Set Table	Existing Employee Import
Source of Import	Select File
Sheet Number	1
Header Row	1
Select the updated Excel file and click Submit.
The sample test data includes:
Existing employee records with changed values.
New employee IDs.
Changed employee names.
Changed email addresses.
After submission, the Import Set should show a completed and successful state.
Run the Transform
Click:
```text
Run Transform
```
The previously created Transform Map should be selected.
Click:
```text
Transform
```
After the transformation, open Transform History to review the results.
Example Result
The documented test contains four uploaded rows:
```text
4 rows uploaded
│
├── 2 rows inserted
│     └── New Employee IDs
│
└── 2 rows updated
      └── Existing Employee IDs
```
The Employee Test table can then be opened to verify the inserted and updated records.
Repeating the Same Import
When the same spreadsheet is uploaded again using the same Transform Map, the documented result is:
```text
4 rows uploaded
│
├── 0 Inserted
├── 0 Updated
└── 4 Ignored
```
This demonstrates the duplicate-handling behavior configured through Coalesce.
---
Phase 8: Create Reports
The project creates three reports from the Employee Test table.
Navigation
```text
All → Reports
Usage and Governance → Reports
```
Click New.
---
📊 Report 1: Employees by Department
Configuration
Property	Value
Report Name	Employees by Department
Source Type	Table
Table	Employee Test
Type	Pie Chart
Group By	Department
Aggregation	Count
Steps
Create a new report.
Enter the report name.
Select Employee Test as the table.
Select Pie Chart.
Configure Group by Department.
Select Count as the aggregation.
Run the report.
Save the report.
---
📊 Report 2: Employees by Location
Configuration
Property	Value
Report Name	Employees by Location
Table	Employee Test
Type	Bar Chart
Group By	Location
Aggregation	Count
Steps
Create a new report.
Enter Employees by Location as the report name.
Select Employee Test.
Select Bar Chart.
Group the report by Location.
Set aggregation to Count.
Run the report.
Save it.
---
📋 Report 3: Employee List Report
Configuration
Property	Value
Report Name	Employee List Report
Table	Employee Test
Type	List
Columns
Employee ID
Employee Name
Email
Department
Location
Run and save the report.
---
Phase 9: Add Reports to Dashboard
Create Dashboard
Navigation
```text
All → Dashboards
Self Service → Dashboards
```
Click Create Dashboards or create the dashboard using:
```text
PA_DASHBOARDS.FORM
```
Dashboard Name
```text
Employee Analytics Dashboards
```
Save the dashboard.
> The source document notes that access to the backend dashboard form may require the appropriate `pa_dashboards` ACL access with Admin Overrides enabled.
---
📈 Add Reports to Dashboard
Open the previously created reports.
Navigation
```text
All → Reports
Usage and Governance → Reports
```
Open:
```text
Employees by Department
```
Then:
```text
Edit Report
      ↓
Share
      ↓
Add to Dashboards
      ↓
Employee Analytics Dashboards
      ↓
Add
```
Repeat the same process for:
Employees by Location
Employee List Report
Dashboard Structure
```text
┌──────────────────────────────────────────┐
│      Employee Analytics Dashboards       │
├───────────────────┬──────────────────────┤
│ Employees by      │ Employees by         │
│ Department        │ Location             │
│ (Pie Chart)       │ (Bar Chart)          │
├───────────────────┴──────────────────────┤
│                                          │
│          Employee List Report            │
│                                          │
└──────────────────────────────────────────┘
```
Reports can also be added using the dashboard's + icon.
The dashboard can additionally be configured with background settings and access restrictions for users, groups, and roles.
---
🧪 Testing & Validation
The project validates the following:
Initial Import
```text
Excel
  ↓
Import Set
  ↓
Transform Map
  ↓
Employee Test
  ↓
Records Created
```
Import with Existing + New Data
```text
4 Excel Rows
     │
     ├── 2 Existing IDs → Updated
     │
     └── 2 New IDs      → Inserted
```
Repeated Import
```text
Same 4 Rows
     │
     ├── 0 Inserted
     ├── 0 Updated
     └── 4 Ignored
```
This verifies the duplicate-handling behavior described in the project.
---
📊 Project Reports
The dashboard provides visibility into employee information through:
Employees by Department
Employees by Location
Employee List Report
The project documentation also identifies reporting around:
Total employee records
Newly added employees
Updated employee records
Department-wise employee distribution
Import success and error counts
---
✅ Final Outcome
The project implements an employee data management workflow using ServiceNow Import Sets and Transform Maps.
The completed workflow supports:
📥 Spreadsheet data import
🗃️ Staging through an Import Set table
🔄 Source-to-target field mapping
♻️ Updating existing employee records
🛡️ Duplicate prevention using Coalesce
📊 Employee reports
📈 Centralized dashboard visualization
The final dashboard provides a centralized view of employee data and import-related information.
---
🧠 Key Concepts Learned
Concept	Purpose
Import Set	Loads external data into ServiceNow staging
Import Set Table	Stores imported source data
Transform Map	Defines how source data is transferred to the target table
Field Map	Maps source fields to target fields
Coalesce	Identifies existing records and prevents duplicates
Transform	Executes the data transformation
Transform History	Helps review transformation results
Reports	Provides visual/data-based analysis
Dashboard	Combines reports into a centralized view
---
📁 Project Structure
A suggested documentation structure for this project is:
```text
Import-Data-Using-Transform-Maps/
│
├── README.md
├── Sample Spreadsheet.xlsx
└── screenshots/
    ├── custom-table.png
    ├── import-set.png
    ├── transform-map.png
    ├── coalesce.png
    ├── reports.png
    └── dashboard.png
```
---
🎓 Conclusion
This project demonstrates an end-to-end employee data import process in ServiceNow using Import Sets and Transform Maps.
Coalesce is an important enhancement because it allows existing employee records to be identified during repeated imports, preventing redundant records and allowing existing information to be updated.
The project is further extended with Reports and Dashboards, providing a centralized visual representation of employee data and import activity.
---
👨‍💻 Project Type
ServiceNow Micro Project
Topic
Import Data Using Transform Maps (Spreadsheet)
Main Technologies
```text
ServiceNow
Import Sets
Transform Maps
Coalesce
Reports
Dashboards
Excel / Google Spreadsheet
```
