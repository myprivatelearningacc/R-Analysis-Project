R Analysis Project – COVID-19 Patient Identification & Healthcare Data Analysis
Author

Nguyen Khanh Ngoc
R Markdown Analytical Report

***Project Overview***

This project performs exploratory data analysis and patient-level investigation using healthcare datasets from two different sources (PG1 and PG2). The primary objective is to integrate, clean, and analyze patient medical records to identify COVID-19 cases and generate meaningful insights from the combined data.

The analysis is conducted in R using an R Markdown (.Rmd) workflow to ensure reproducibility and structured reporting.

***Project Structure***
.
├── R analysis.Rmd
├── data
  └── patientsPG1.csv
  └── patientsPG2.csv
  └── encountersPG1.csv
  └── encountersPG2.csv
  └── conditionsPG1.csv
  └── conditionsPG2.csv
├── README.md

***Objectives***

The project focuses on:

Data Integration

Import six raw datasets (patients, encounters, conditions from PG1 and PG2).

Merge them into three unified datasets.

Standardize column names.

Validate structure and row counts.

Data Cleaning & Preparation

Convert date fields to appropriate Date format.

Handle missing values (e.g., empty death dates).

Compute derived variables (e.g., patient age).

COVID-19 Patient Identification

Detect condition records containing the keyword "COVID" (case-insensitive).

Extract distinct patient IDs.

Compute total number of unique COVID-related patients.

Visualize relevant results.

Exploratory Analysis

Analyze patient demographics.

Explore encounter and condition distributions.

Generate visual summaries using ggplot2.

Technologies & Libraries Used

The project is implemented in R, using the following libraries:

dplyr – Data manipulation

stringr – String processing

lubridate – Date handling

ggplot2 – Data visualization

knitr – Report generation

***Data Processing Workflow***
Step 1 – Data Import & Merging

Each dataset is:

Imported separately.

Tagged with a source indicator (PG1, PG2).

Row-bound into unified tables:

patients

encounters

conditions

Step 2 – Standardization

All column names converted to lowercase.

Dates converted to Date objects.

Age calculated using:

Age = as.numeric(difftime(Sys.Date(), birthdate, units = "days")) / 365.25


(Using 365.25 to account for leap years.)

Step 3 – COVID-19 Identification

Patients are classified as COVID-related if:

The description field in the conditions dataset contains the term "COVID" (case-insensitive).

Unique patient IDs are extracted to prevent duplication.

***Assumptions***

Any condition containing the string "COVID" qualifies as COVID-related (e.g., COVID-19, Suspected COVID, etc.).

Patients may have multiple encounters; therefore, analysis is performed using distinct patient IDs.

Empty death dates are treated as NA.

***How to Run the Project***

Clone the repository:

git clone <your-repo-link>


Open R analysis.Rmd in RStudio.

Ensure all required .csv files are in the working directory.

Knit the document to:

Word document

PDF document

***Output***

The R Markdown file generates:

Cleaned and merged datasets

Summary statistics

COVID patient counts

Visualizations

Reproducible analytical documentation

***Key Strengths of This Project***

Reproducible workflow using R Markdown

Clear data integration pipeline

Structured cleaning and transformation steps

Transparent assumptions

Professional reporting format
