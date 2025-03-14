# Data-Analysis-Power-BI
# Power BI Report Documentation: Analyzing Student Data for ABC Institute (2021–2023)

## 1. Introduction

This document details the creation of an interactive Power BI report analyzing student data from the "ABC Institute" for the years 2021–2023.  The report provides insights into:

*   The total number of students trained each year.
*   The total fees collected, broken down by course and month.
*   The number of certificates issued to students.
*   The distribution of students by age group and city.

**What is Power BI?**  Power BI is a Business Intelligence tool by Microsoft that allows users to import data from various sources, clean and transform it, and create interactive visualizations and reports. Its user-friendly interface and powerful features make it ideal for this type of analysis.

## 2. Prerequisites

Before starting the project, the following were required:

*   **Software:** Power BI Desktop (freely available from Microsoft).
*   **Data Sources:**
    *   Three text files containing course details (e.g., Student ID, Name, Age, Course, Date of Joining, Fees).
    *   One Excel workbook with personal details (e.g., Name, Age, Contact Number, Email, City, Certificate Issued).

## 3. Installation of Power BI Desktop

Power BI Desktop was installed using one of the following methods:

**Option 1: Microsoft Store**

1.  Opened the Microsoft Store from the Start menu.
2.  Searched for "Power BI Desktop."
3.  Clicked "Get" to download and install it.

**Option 2: Official Website**

1.  Searched "Power BI Desktop download" in a web browser.
2.  Visited the official Microsoft Power BI website and downloaded the installer.
3.  Ran the installer and followed the on-screen instructions.

After installation, Power BI Desktop was launched from the Start menu, and the welcome screen was closed to begin working.

## 4. Importing Data

Power BI supports importing data from multiple sources.  This project involved importing data from text files and an Excel workbook.

**Importing Text Files (Course Details)**

1.  Opened Power BI Desktop and navigated to the **Home** tab.
2.  Clicked **Get Data > Text/CSV**.
3.  Because there were multiple text files, **Folder** was selected instead of individual files.
4.  Browsed to the folder containing the text files and clicked **OK**.
5.  In the preview window, **Combine and Transform Data** was chosen to merge the files and open them in Power Query Editor for cleaning.

**Importing Excel Workbook (Personal Details)**

1.  In Power BI Desktop, clicked **Get Data > Excel Workbook**.
2.  Browsed to the Excel file and selected it.
3.  In the **Navigator** window, the table containing the personal details data was selected.
4.  Clicked **OK** to load it into Power Query Editor for further processing.

## 5. Data Cleaning

Data cleaning is crucial for accurate analysis. Power Query Editor was used to clean both datasets.

**Cleaning Course Details (Text Files)**

*   **Preview:** The combined text files had tab-separated columns (e.g., Source Name, Student ID, Name+Age, Contact, Email, Course, Date of Joining, Fees).

*   **Steps:**

    1.  **Removed Unnecessary Columns:** Selected "Source Name," "Student ID," "Contact," and "Email" columns, then went to **Home > Remove Columns**.
    2.  **Split Name+Age Column:** Right-clicked the "Name+Age" column, selected **Split Column > By Digit to Non-Digit** to separate Name and Age.
    3.  Renamed "Column2.1" to "Student Name" and capitalized each word (**Transform > Format > Capitalize Each Word**).
    4.  Renamed "Column2.2" to "Age" and set the data type to **Whole Number**.
    5.  **Renamed Remaining Columns:**
        *   "Column5" to "Course."
        *   "Column6" to "Date of Joining" (set format to **Date**).
        *   "Column7" to "Fees."
    6.  **Cleaned Fees Column:** Split the "Fees" column by space to remove the "Rs" prefix.  Removed the "Rs" column.  Renamed the remaining column to "Fees" and set the data type to **Whole Number**.
    7.  **Removed Duplicates:** Right-clicked the "Student Name" column and selected **Remove Duplicates**.

**Cleaning Personal Details (Excel)**

*   **Preview:** Columns included Student Name, Age, Contact Number, Email, City, Issued Certificate (Yes/No).

*   **Steps:**

    1.  Confirmed the data was well-structured and required no major cleaning.
    2.  Renamed the table to "Personal Details" for clarity.
    3.  Verified there were no duplicates.

**Finalizing Data**

Clicked **Close & Apply** in Power Query Editor to load both cleaned tables into Power BI.

## 6. Data Modeling

Data modeling connects the tables to enable combined analysis.

1.  Switched to **Model View** in Power BI.
2.  Power BI automatically detected a relationship between the "Student Name" columns in the "Course Details" and "Personal Details" tables.
3.  If no relationship had existed, a one-to-one relationship would have been manually created by dragging "Student Name" from "Course Details" to "Personal Details."
4.  Ensured there were no duplicate or blank values in the "Student Name" column to maintain data integrity.

## 7. Building the Report

With the data prepared, the report was built by creating visualizations to display the required insights.

**Initial Setup**

1.  Saved the file: **File > Save As** > Named it "ABC Institute Report" > Saved to Desktop.
2.  Renamed the page: Double-clicked "Page 1" > Named it "ABC Institute Report."

**Visualizations**

*   **Column Chart: Course Count by Month**
    *   Added a **Clustered Column Chart**.
    *   **X-Axis:** "Date of Joining" (drilled down to Month).
    *   **Y-Axis:** "Course" (set aggregation to **Count**).
    *   **Formatting:** Removed axis titles, added data labels.

*   **Donut Chart: Courses by Age Group**
    *   Added a **Donut Chart**.
    *   **Legend:** "Age" (created bins/groups: Below 20, 20–29, 30–39, 40+).  *(Note:  Creating bins/groups is done in the Modeling tab or within the visual itself.)*
    *   **Values:** "Course" (set aggregation to **Count**).
    *   **Formatting:** Moved legend to the bottom, bolded labels.

*   **Bar Chart: Fees by Course**
    *   Added a **Clustered Bar Chart**.
    *   **Y-Axis:** "Course."
    *   **X-Axis:** "Fees" (set aggregation to **Sum**).
    *   **Formatting:** Adjusted height, copied formatting from the Column Chart (using the Format Painter).

*   **Card: Total Amount**
    *   Added a **Card**.
    *   **Field:** "Fees" (set aggregation to **Sum**).
    *   **Formatting:** Set title to "TOTAL AMOUNT," displayed units in thousands.

*   **Card: Total Students**
    *   Added another **Card**.
    *   **Field:** "Student Name" (set aggregation to **Count**).
    *   **Formatting:** Set title to "TOTAL STUDENTS," matched formatting with the "Total Amount" card.

*   **Gauge: Certificates Issued**
    *   Added a **Gauge**.
    *   **Value:** Created a measure to count "Yes" in the "Issued Certificate" column.  *(Example DAX measure: `Certificates Issued = CALCULATE(COUNT('Personal Details'[Issued Certificate]), 'Personal Details'[Issued Certificate] = "Yes")`)*
    *   **Maximum:** Set to the total count of "Issued Certificate" (another measure could be used here). *(Example DAX measure: `Total Certificates = COUNT('Personal Details'[Issued Certificate])`)*
    *   **Formatting:** Removed the target line if unnecessary.

*   **Slicers: Filters**
    *   Added slicers for **Year**, **City**, and **Course**.
    *   Set slicer style to **Dropdown**.
    *   Arranged the slicers at the top of the report.

**Final Touches**

*   **Interactivity:** Enabled cross-filtering by clicking on visuals (this is usually on by default).
*   **Lock Objects:** Went to **View > Lock Objects** to prevent accidental changes.
*   **Theme:** Applied a suitable theme from **View > Themes**.

## 8. Additional Features

To enhance the report, the following were implemented:

*   **Mobile Layout:** Navigated to **View > Mobile Layout** and rearranged visuals for optimal mobile viewing.
*   **Publishing:** Went to **Home > Publish**, signed in, and shared the report online.
*   **Background:** Customized the report background (optional) for a polished look.

## 9. Conclusion

This project successfully demonstrates the creation of a comprehensive Power BI report from scratch. The process covered data importation, cleaning, modeling, and visualization, providing valuable insights into student enrollment, fees collection, and certification trends at ABC Institute from 2021 to 2023. The final report is interactive, visually appealing, and beginner-friendly.
