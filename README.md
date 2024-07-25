# Cyclistic Bike Share Analysis
<img width="671" alt="Screenshot 2024-07-24 at 7 26 08 PM" src="https://github.com/user-attachments/assets/a29c67c8-da6a-47a8-be44-eba6e524d8d6">

*This project was done to complete the [Google Data Analytics Certification](https://www.coursera.org/professional-certificates/google-data-analytics) on Coursera. The names of the company and any individuals mentioned here are entirely fictional, but the analysis uses a real dataset provided under a public license.*

## Overview and Analysis Approach

Cyclistic, founded in 2016, operates a successful bike-share program in Chicago, featuring 5,824 geotracked bicycles distributed across 692 stations. The company offers flexible pricing plans, including single-ride passes, full-day passes, and annual memberships. The strategic goal is to convert casual riders into more profitable annual members. The marketing director aims to maximize annual memberships by analyzing usage patterns between casual riders and annual members, and using these insights to craft a targeted conversion strategy, supported by data-driven recommendations and visualizations for executive approval. <br>

This analysis will adhere to the standard data analysis process, which includes the following steps: ask, prepare, process, analyze, share, and act. <br>

*Let's dive in...*

## 1. Ask

### 1.1 What are the business objectives?

* Understand the usage patterns of annual members and casual riders with Cyclistic bikes.
* Identify motivations for casual riders to purchase Cyclistic annual memberships.
* Develop strategies utilizing digital media to encourage casual riders to transition into annual members at Cyclistic.

### 1.2. Who are the key Stakeholders?

* Cyclistic Executive Team: Approves marketing programs; interested in profitability and growth.
* Lily Moreno: Marketing director; aims to convert casual riders into annual members.
* Cyclistic Marketing Analytics Team: Analyzes data to guide marketing strategies.

### 1.3. What are the deliverables of this whole analysis?

1. A clear statement of the business task,
2. A description of all data sources used,
3. Documentation of any cleaning or manipulation of data,
4. A summary of the analysis,
5. Supporting visualizations and key findings,
6. Top three recommendations based on the analysis.

## 2. Prepare

### 2.1. Business Tasks

Analyze how casual riders and annual members use Cyclistic bikes differently and use this data to recommend a strategy for converting casual riders into annual members.

### 2.2. Data Source

For this analysis, I used historical trip data covering January 2020 to June 2024. The dataset includes:
* File Details: 52 .csv files
* Contents: Trip start and end times, start and end stations, and rider type (Member, Single Ride, Day Pass)
* Data Size: 22,929,303 rows and 13 columns (9 text, 4 float64)

### 2.3. ROCCC

[The dataset]((https://divvybikes.com/system-data)) is reliable, original, comprehensive, current, and properly cited.  It is released under a public [license]((https://www.divvybikes.com/data-license-agreement)) that permits analysis while protecting personally identifiable information (e.g., credit card details, addresses). The data is updated monthly. To ensure quality, trips taken by staff and those shorter than 60 seconds have been excluded by the source.

## 3. Process

### 3.1. Tools

This analysis utilizes Python for data processing, specifically to combine the 52 .csv files into a single .csv file. Python is also employed for data cleaning and manipulation to ensure the dataset is prepared and ready for analysis.

### 3.2. Combining Multiple .csv Files

To consolidate the 52 .csv files into a single dataset, Python's pandas library is used. This process involves:
* **Listing the Files**: Identifying all .csv files in the dataset folder.
* **Loading the Files**: Reading each .csv file into separate DataFrames.
* **Merging Data**: Combining these DataFrames into one comprehensive DataFrame.
* **Checking Metadata**: Verifying column names, data types, and consistency across the DataFrames.
* **Saving the Consolidated Data**: Exporting the combined DataFrame into a single .csv file for further analysis. This method ensures that all data is unified and readily accessible for subsequent cleaning and analysis.


