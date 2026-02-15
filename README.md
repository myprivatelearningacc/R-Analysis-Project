COVID-19 Patient Identification and Healthcare Data Analysis (R)
Author

Nguyen Khanh Ngoc

Project Overview

This project performs exploratory data analysis and patient-level investigation using healthcare datasets from two different sources (PG1 and PG2).

The primary objective is to integrate, clean, and analyze patient medical records to identify COVID-19 cases and generate structured insights from the combined data.

The entire workflow is implemented in R using an R Markdown (.Rmd) file to ensure reproducibility and clarity.

Objectives
Data Integration

Import six datasets (patients, encounters, and conditions from PG1 and PG2)

Merge datasets into unified tables

Standardize column names

Validate structure and row counts

Data Cleaning and Preparation

Convert date variables to proper Date format

Handle missing values

Compute derived variables (e.g., patient age)

COVID-19 Patient Identification

Detect condition records containing the keyword "COVID" (case-insensitive)

Extract distinct patient IDs

Compute the total number of unique COVID-related patients

Exploratory Analysis

Analyze patient demographics

Examine condition and encounter distributions

Generate visualizations using ggplot2

Dataset Overview
1. Patients Dataset

Patient demographic data.

id — Unique identifier of the patient

BirthDate — Date the patient was born

DeathDate — Date the patient died (empty indicates patient is still alive)

Marital — Marital status (M = Married, S = Single)

Race — Description of the patient’s primary race

Gender — Gender (M = Male, F = Female)

City — City of the patient’s current address

State — State of the patient’s current address

County — County of the patient’s current address

Zip — Postal code

2. Encounters Dataset

Patient encounter data.

id — Unique identifier of the encounter

Start — Date and time the encounter started

Stop — Date and time the encounter concluded

Patient — Patient ID

EncounterClass — Type of encounter (ambulatory, emergency, inpatient, wellness, urgent care)

Code — Encounter code using SNOMED-CT

Description — Description of the encounter type

Base Encounter Cost — Base cost excluding additional services

Total Claim Cost — Total cost including all services

Payer Coverage — Amount covered by payer

ReasonCode — Diagnosis code from SNOMED-CT (if applicable)

ReasonDescription — Description of the diagnosis

3. Conditions Dataset

Patient diagnoses or conditions.

Start — Date the condition was diagnosed

Stop — Date the condition resolved (if applicable)

Patient — Patient ID

Encounter — Encounter ID linked to this diagnosis

Code — Diagnosis code from SNOMED-CT

Description — Description of the diagnosis/condition

Technologies and Libraries

This project is implemented in R and uses the following libraries:

dplyr — Data manipulation

stringr — String processing

lubridate — Date handling

ggplot2 — Data visualization

knitr — Report generation

Data Processing Workflow
1. Data Import and Merging

Each dataset is imported separately and assigned a source indicator (PG1 or PG2).

The datasets are combined using row binding to create three unified tables:

patients

encounters

conditions

2. Standardization

Column names are converted to lowercase

Date fields are converted to Date objects

Age is calculated using:

Age <- as.numeric(difftime(Sys.Date(), birthdate, units = "days")) / 365.25


The factor 365.25 accounts for leap years.

3. COVID-19 Identification

Patients are classified as COVID-related if the description field in the conditions dataset contains the term "COVID" (case-insensitive).

Distinct patient IDs are extracted to ensure each patient is counted only once.

Assumptions

Any condition containing the string "COVID" qualifies as COVID-related

Patients may have multiple encounters; analysis is performed at the patient level using distinct IDs

Empty death dates are treated as missing values (NA)
