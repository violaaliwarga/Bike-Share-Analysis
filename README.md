# From Rides to Members: Analyzing Cyclistic Bike-Share Data for Membership Predictions
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

### 3.3. Data Cleaning & Manipulation

Handling missing data is a critical step in data cleaning and manipulation, especially with historical datasets like the Cyclistic Bike-Share data. Missing data can arise from various factors, including human error, system glitches, or incomplete data collection processes. Here’s a detailed approach to how I dealt with the missing values:

#### 3.3.1. Checking for Missing Data
First, I checked for the presence of missing data in the dataset. Here are what I got:
<img width="318" alt="Screenshot 2024-07-30 at 3 40 29 PM" src="https://github.com/user-attachments/assets/36a1ff23-5b1f-4e8e-abf0-656efc7cf746">

#### 3.3.2. Identify Missing Data
To effectively handle missing data, it's essential to first determine the extent of missing values in each column. This step informs the appropriate methods for addressing the missing data. Here’s how I approached it:

##### a. Flagging Missing Data
I flagged the missing values in each column by converting False (no missing value) and True (missing value) to 0 and 1, respectively. This conversion is crucial because it transforms the missing data indicators into numerical values, which are necessary for subsequent analysis.

##### b. Visualizing Missing Data Distribution
I plotted the distribution of missing values to identify patterns and the extent of missing data across the dataset. Here's the result:
<img width="407" alt="Screenshot 2024-07-30 at 3 49 00 PM" src="https://github.com/user-attachments/assets/7e0a898c-a383-4d1a-b0e1-ea1522ca4021">

##### c. Analyzing Correlations
I also checked the correlation between the variables to understand how missing values might relate to other features in the dataset.
<img width="588" alt="Screenshot 2024-07-30 at 3 49 55 PM" src="https://github.com/user-attachments/assets/10d5a4e5-34f2-4663-9940-d35019a9742a">
As shown in the picture above, the correlation coefficients ranged from -0.01 to 1.0. What does it mean? A coefficient close to 0, such as -0.01, indicates a very weak relationship between the variables. In this case, missing data in one column has little to no correlation with missing data in other columns. Whereas a coefficient of 1.0 suggests a perfect positive correlation, meaning that if one column has missing data, the other column will also have missing data in exactly the same pattern.


The output and the complete code for these steps are available in a separate file [here]. This detailed analysis of missing data helped guide the subsequent data cleaning and imputation strategies, ensuring a thorough and methodical approach to preparing the dataset for analysis.
