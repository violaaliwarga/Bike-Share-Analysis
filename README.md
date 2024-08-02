# From Rides to Members: Analyzing Cyclistic Bike-Share Data for Membership Predictions
<img width="671" alt="Screenshot 2024-07-24 at 7 26 08 PM" src="https://github.com/user-attachments/assets/a29c67c8-da6a-47a8-be44-eba6e524d8d6">

*This project was done to complete the [Google Data Analytics Certification](https://www.coursera.org/professional-certificates/google-data-analytics) on Coursera. The names of the company and any individuals mentioned here are entirely fictional, but the analysis uses a real dataset provided under a [public license](https://www.divvybikes.com/data-license-agreement).*

*The output and the complete code for all these steps are available in a separate file [here].*

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
* **Listing the Files**: Identifying all .csv files in the dataset folder using `os.listdir()`. <br>
  <img width="166" alt="Screenshot 2024-08-02 at 10 38 48 AM" src="https://github.com/user-attachments/assets/9aa2d59a-b649-4474-95b4-750878dcedb0"> <br>
* **Loading the Files**: Reading each .csv file into separate DataFrames using `pd.read_csv()`.
* **Merging Data**: Combining these DataFrames into one comprehensive DataFrame using `pd.concat()`.<br>
  <img width="249" alt="Screenshot 2024-08-02 at 10 39 24 AM" src="https://github.com/user-attachments/assets/f285c4f9-fc97-4c03-82f1-833f50882d3c"> <br>
* **Saving the Consolidated Data**: Exporting the combined DataFrame into a single .csv file using `DataFrame.to_csv()` for further analysis. This ensures that all data is unified and readily accessible for subsequent cleaning and analysis.

### 3.3. Data Cleaning & Manipulation

Handling missing data is a critical step in data cleaning and manipulation, especially with historical datasets like the Cyclistic Bike-Share data. Missing data can arise from various factors, including human error, system glitches, or incomplete data collection processes. Here’s a detailed approach to how I dealt with the missing values:

#### 3.3.1. Checking for Missing Data
First, I checked for the presence of missing data in the dataset using `pandas.isnull()`. Here's what I got: <br>
<img width="199" alt="Screenshot 2024-08-02 at 10 39 39 AM" src="https://github.com/user-attachments/assets/1a73aaa5-ea8b-4757-b007-9b766b7a8d3e">

#### 3.3.2. Identify Missing Data
To effectively handle missing data, it's essential to first determine the extent of missing values in each column. This step informs the appropriate methods for addressing the missing data. Here are the steps that I took:

##### a. Flagging Missing Data
I flagged the missing values in each column by converting False (no missing value) and True (missing value) to 0 and 1, respectively, using `pandas.astype()`. This conversion is crucial because it transforms the missing data indicators into numerical values, which are necessary for subsequent analysis.

##### b. Visualizing Missing Data Distribution
I plotted the distribution of missing values using Matplotlib `plot()` function to identify patterns and the extent of missing data across the dataset. Here's the result: <br>
<img width="306" alt="Screenshot 2024-08-02 at 10 39 53 AM" src="https://github.com/user-attachments/assets/9696c162-5862-46de-9192-b6f05c5351dd">

##### c. Analyzing Correlations
I also checked the correlation between the variables, using Pandas `DataFrame.corr()`, to understand how missing values might relate to other features in the dataset. <br>
<img width="471" alt="Screenshot 2024-08-02 at 10 40 09 AM" src="https://github.com/user-attachments/assets/32370240-a1f6-4f4f-a42a-fab22f3071c0"> <br>
As shown in the picture above, the correlation coefficients ranged from -0.01 to 1.0. What does it mean? A coefficient close to 0, such as -0.01, indicates a very weak relationship between the variables. In this case, missing data in one column has little to no correlation with missing data in other columns. Whereas a coefficient of 1.0 suggests a perfect positive correlation, meaning that if one column has missing data, the other column will also have missing data in exactly the same pattern.

#### 3.3.3. Handling Missing Data
After the steps above and analyzing the results, I decided on two approaches regarding on what I was going to do to those missing data.

##### a. Removing Rows with Missing Values
For the columns **`end_lat`** and **`end_lng`**, I decided to remove the rows with missing values. This decision is based on the small amount of missing data in these columns (only 0.1%) and the correlation of these variables with other columns that also have missing data, as seen above in Section 3.3.2.c..

##### b. Imputing Missing Values using K-nearest neighbors (KNN)
I noticed a substantial amount of missing data, more than 5%, in the columns **`start_station_name`**, **`start_station_id`**, **`end_station_name`**, and **`end_station_id`**. Since these columns tell us where each bike trip starts and ends, they’re really important for the analysis. Instead of just getting rid of the incomplete records, I decided to fill in the missing data using a method called K-nearest neighbors (KNN).

A little bit about KNN. KNN is a machine learning technique based on a simple idea: data points that are close to each other tend to be similar. So, if some station info is missing, we can look at the closest data points to make an educated guess. This method is particularly handy here because station names and IDs that are near each other usually correspond to nearby trips. Here’s how I went about it:

1. Preprocess the Data
First, I made a list of columns that shouldn’t be scaled or imputed (non-categorical variables). Then, I used `LabelEncoder` to convert categorical columns into numerical values, which is necessary for KNN to work. I excluded columns like `ride_id` and datetime columns from this step. Finally, I listed the columns that actually needed imputation.

2. Apply KNN Imputation
Although optional, I normalized the data to ensure that all features contributed equally to the KNN calculations. Then, I used the KNN algorithm to fill in the missing values by looking at the nearest data points. After imputing the missing values, I reversed the scaling to bring the data back to its original scale.

3. Post-process the Data
I converted any numerical columns that were originally categorical back to their original form. I then reattached the columns that were excluded from the scaling and imputation process. Finally, I reviewed the newly completed DataFrame to ensure everything was in order. <br>

By using KNN, I was able to fill in the missing station data accurately, keeping the dataset intact and making sure my analysis remained reliable. <br>

<img width="219" alt="Screenshot 2024-08-02 at 10 41 12 AM" src="https://github.com/user-attachments/assets/c0b8f2d7-8ffe-43ec-a5f9-0513ffe216fa"> <br>

<img width="145" alt="Screenshot 2024-08-02 at 10 41 32 AM" src="https://github.com/user-attachments/assets/17ab6deb-b8ab-4a31-83c5-6f8dddf7373a"> <br>

#### 3.3.4. Creating New Columns Necessary for Analysis

##### a. Assigning Appropriate DataType to `started_at` & `ended_at`
To be able to do what i want to do next, i have to convert the two columns to datetime datatype. <br>
<img width="272" alt="Screenshot 2024-08-02 at 10 41 43 AM" src="https://github.com/user-attachments/assets/1e00788d-038e-4a73-b5e8-b201265bbdbf">

##### b. Creating New Columns `month`, `day`, `hour`, and `duration_minutes`
To complete my analysis in the next step, i would like to make new columns.
<img width="328" alt="Screenshot 2024-08-02 at 10 42 04 AM" src="https://github.com/user-attachments/assets/977441ae-9531-4ff1-9299-7c9d28a59583">
