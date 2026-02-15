COVID-19 Patient Identification and Healthcare Data Analysis (R)
Author

Nguyen Khanh Ngoc

Project Overview

This project performs exploratory data analysis and patient-level investigation using healthcare datasets from two different sources (PG1 and PG2). The primary objective is to integrate, clean, and analyze patient medical records to identify COVID-19 cases and generate structured insights from the combined data.

The entire workflow is implemented in R using an R Markdown (.Rmd) file to ensure reproducibility and clarity.

Objectives

This project focuses on the following:

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

Dataset overview: 
patients: Patient demographic data:
– id – the unique identifier of the patient.
– BirthDate – The date the patient was born.
– DeathDate – The date the patient died. An empty field indicates the patient is still alive.
– Marital – The patient’s marital status. M - Married and S - Single.
– Race – Description of the patient’s primary race.
– Gender – Gender. M is male, and F is female.
– City – The city of the patient’s current address.
– State – The state of the patient’s current address.
– County – The county of the patient’s current address.
2

– Zip – The postal code for the patient.
Encounters: Patient encounter data.
– id – the unique identifier of the encounter
– Start – The date and time the encounter started.
– stop – The date and time the encounter concluded.
– Patient – The patient ID for the patient who went to health services
– EncounterClass –The type of encounter, such as, ambulatory, emergency, inpatient, wellness,
or urgent care.
– Code – The Encounter code using the Health Standard coding of SNOMED-CT (More info at
https://www.snomed.org/).
– Description – Description of the type of encounter.
– Base Encounter Cost – The base cost of the encounter, not including any line item costs
related to medications, immunisations, procedures and or other services.
– Total Claim Cost – The total cost of the encounter, including all line items.
– Payer Coverage – The amount of cost the Payer covers.
– ReasonCode – The Diagnosis code from SNOMED-CT, if this encounter targeted a specific
condition.
– ReasonDescription – Description of the reason code.
conditions: Patient conditions or diagnoses.
– Start – The date the condition was diagnosed.
– Stop – The date the condition resolved, if applicable.
– Patient – Patient ID for the diagnosed patient.
– Encounter – Encounter ID to map the encounter details for this patient.
– Code – Diagnosis code from SNOMED-CT.
– Description – The description of the diagnosis/condition.

Technologies and Libraries

The project is implemented in R and uses the following libraries:

dplyr — data manipulation

stringr — string processing

lubridate — date handling

ggplot2 — data visualization

knitr — report generation

Data Processing Workflow
1. Data Import and Merging

Each dataset is imported separately and assigned a source indicator (PG1 or PG2).
The datasets are then combined using row binding to create three unified tables:

patients

encounters

conditions

2. Standardization

Column names are converted to lowercase

Date fields are converted to Date objects

Age is calculated using:

Age = as.numeric(difftime(Sys.Date(), birthdate, units = "days")) / 365.25


The factor 365.25 accounts for leap years.

3. COVID-19 Identification

Patients are classified as COVID-related if the description field in the conditions dataset contains the term "COVID" (case-insensitive).

Distinct patient IDs are extracted to ensure each patient is counted only once.

Assumptions

Any condition containing the string "COVID" qualifies as COVID-related.

Patients may have multiple encounters, so analysis is performed at the patient level using distinct IDs.

Empty death dates are treated as missing values (NA).
