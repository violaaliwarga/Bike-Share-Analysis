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

For this analysis, I used Python 3 in Jupyter Notebook to process the data, including combining 52 separate .csv files into one comprehensive dataset. Python was also essential for cleaning and preparing the data for further analysis. I then utilized PostgreSQL to perform further analysis according to my project objectives. Finally, I will use Tableau Public to visualize and present my findings.

### 3.2. Combining Multiple .csv Files

To consolidate the 52 .csv files into a single dataset, Python's pandas library is used. This process involves:
* **Listing the Files**: Identifying all .csv files in the dataset folder using `os.listdir()`. <br>
  <img width="166" alt="Screenshot 2024-08-02 at 10 38 48 AM" src="https://github.com/user-attachments/assets/9aa2d59a-b649-4474-95b4-750878dcedb0"> <br>
* **Loading the Files**: Reading each .csv file into separate DataFrames using `pd.read_csv()`.
* **Merging Data**: Combining these DataFrames into one comprehensive DataFrame using `pd.concat()`.<br>
  <img width="249" alt="Screenshot 2024-08-02 at 10 39 24 AM" src="https://github.com/user-attachments/assets/f285c4f9-fc97-4c03-82f1-833f50882d3c"> <br>
* **Saving the Consolidated Data**: Exporting the combined DataFrame into a single .csv file using `DataFrame.to_csv()` for further analysis. This ensures that all data is unified and readily accessible for subsequent cleaning and analysis.

### 3.3. Data Cleaning & Manipulation

Handling missing data is a critical step in preparing and manipulating datasets, especially when working with historical data like the Cyclistic Bike-Share dataset. Missing data can result from various factors such as human error, system glitches, or incomplete data collection. Below, I outline the systematic approach I used to address the missing data in this dataset.

#### 3.3.1. Checking for Missing Data
First, I assessed the presence of missing data in the dataset using pandas.isnull().sum(). The initial inspection revealed the following results: <br>
<img width="199" alt="Screenshot 2024-08-02 at 10 39 39 AM" src="https://github.com/user-attachments/assets/1a73aaa5-ea8b-4757-b007-9b766b7a8d3e">

#### 3.3.2. Identifying and Analyzing Missing Data
To effectively manage missing data, it's crucial to understand both the extent and potential patterns of missing values in each column. Here's the approach I took:

##### a. Flagging Missing Data
I flagged missing values by converting the boolean indicators (False for no missing data, True for missing data) into numerical values (0 for no missing data, 1 for missing data) using pandas.astype(int). This conversion facilitated a more straightforward analysis of the missing data patterns.

##### b. Visualizing the Distribution of Missing Data
Next, I visualized the distribution of missing data across the dataset using Matplotlib to identify any patterns. This visualization helped in understanding how widespread the missing data was and whether any specific columns were disproportionately affected. <br>
<img width="306" alt="Screenshot 2024-08-02 at 10 39 53 AM" src="https://github.com/user-attachments/assets/9696c162-5862-46de-9192-b6f05c5351dd">

##### c. Analyzing Correlations Among Variables
To understand how missing data in one column might relate to another, I calculated the correlation coefficients using pandas.DataFrame.corr(). <br>
<img width="471" alt="Screenshot 2024-08-02 at 10 40 09 AM" src="https://github.com/user-attachments/assets/32370240-a1f6-4f4f-a42a-fab22f3071c0"> <br>

The correlation coefficients ranged from -0.01 to 1.0:
- Near-zero correlation (e.g., -0.01): Indicates a very weak relationship between missing data in different columns, suggesting that missing values in one column don't strongly predict missing values in another.
- Perfect correlation (e.g., 1.0): Indicates a strong relationship, where missing data in one column perfectly aligns with missing data in another.

#### 3.3.3. Handling Missing Data
After the steps above and analyzing the results, I decided on two approaches regarding on what I was going to do to those missing data.

##### a. Removing Rows with Missing Values
For the columns `end_lat` and `end_lng`, I opted to remove rows with missing values. This decision was driven by the fact that less than 1% of the data was missing in these columns, minimizing the impact of data loss on the analysis.

##### b. Imputing Missing Values using K-nearest neighbors (KNN)
Columns `start_station_name`, `start_station_id`, `end_station_name`, and `end_station_id` had more than 10% missing data. Given their importance in identifying trip origins and destinations, I chose to impute the missing values using the K-nearest neighbors (KNN) algorithm.

A little bit about KNN. KNN is based on the principle that data points close to each other in feature space are likely similar. For missing station data, this method is particularly effective because stations that are geographically close often correspond to similar trips. Here’s how I applied KNN:

1. Preprocess the Data
First, I made a list of columns that shouldn’t be scaled or imputed (non-categorical variables). Then, I used `LabelEncoder` to convert categorical columns into numerical values, which is necessary for KNN to work. I excluded columns `ride_id` from this step. Finally, I listed the columns that actually needed imputation.

2. Apply KNN Imputation
Although optional, I normalized the data to ensure that all features contributed equally to the KNN calculations. Then, I used the KNN algorithm to fill in the missing values by looking at the nearest data points. After imputing the missing values, I reversed the scaling to bring the data back to its original scale.

3. Post-process the Data
I converted any numerical columns that were originally categorical back to their original form. I then reattached the columns that were excluded from the scaling and imputation process. Finally, I reviewed the newly completed DataFrame to ensure everything was in order. <br>

Using KNN allowed me to preserve the integrity of the dataset while accurately filling in critical missing values. <br>

<img width="219" alt="Screenshot 2024-08-02 at 10 41 12 AM" src="https://github.com/user-attachments/assets/c0b8f2d7-8ffe-43ec-a5f9-0513ffe216fa"> <br>

<img width="145" alt="Screenshot 2024-08-02 at 10 41 32 AM" src="https://github.com/user-attachments/assets/17ab6deb-b8ab-4a31-83c5-6f8dddf7373a"> <br>

#### 3.3.4. Creating New Columns Necessary for Analysis

##### a. Converting `started_at` and `ended_at` to Datetime Format
To facilitate further analysis, I converted the `started_at` and `ended_at` columns to datetime format. <br>
<img width="272" alt="Screenshot 2024-08-02 at 10 41 43 AM" src="https://github.com/user-attachments/assets/1e00788d-038e-4a73-b5e8-b201265bbdbf">

##### b. Creating New Columns
To dig deeper into the data, I created new columns from the started_at and ended_at information: <br>
- `month`: The month when the ride started. <br>
- `day`: The day of the week when the ride started. <br>
- `hour`: The hour of the day when the ride started. <br>
- `duration_minutes`: The total duration of the ride in minutes. <br>

<img width="328" alt="Screenshot 2024-08-02 at 10 42 04 AM" src="https://github.com/user-attachments/assets/977441ae-9531-4ff1-9299-7c9d28a59583">


## 4. Analysis & Visualization

### 4.1. Findings

#### 4.1.1. How do the total number of rides compare between membership types?
<img width="250" alt="Total Rides_main" src="https://github.com/user-attachments/assets/d17d7ba4-d218-4798-80be-3fad3dd50bd0">
<img width="50" alt="Total Rides_leg" src="https://github.com/user-attachments/assets/d70525e8-f290-47b1-99b6-eb2ae3e96fa0"><br>
Casual riders have made 9,072,123 rides, while annual members have made 13,820,576 rides. This significant difference indicates that annual members engage with the bike-share system more frequently, suggesting either higher engagement or more regular usage among this group.

#### 4.1.2. What is the average ride duration for each membership type?
| Membership Type | Average Duration |
| --- | --- |
| Casual | 28 minutes |
| Annual | 13 minutes |<br>
Casual riders generally take longer rides, while annual members tend to make shorter, more frequent trips.

#### 4.1.3. How does the number of rides vary by day of the week for each membership type?
<img width="500" alt="Rides by Day of the Week" src="https://github.com/user-attachments/assets/03317772-178c-4873-9d87-a579c79bcbb1"> <br>
Casual riders show peak usage on weekends, with the highest number of rides occurring on Saturday (1,920,554) and Sunday (1,606,326). Their lowest usage is observed on Tuesday (1,009,584). In contrast, annual members have their highest usage on Wednesday (2,177,786) and Tuesday (2,119,614), with the lowest on Sunday (1,623,645). This pattern indicates that casual riders are more active during weekends, while annual members use the service more regularly throughout the workweek.

#### 4.1.4. What are the patterns of bike usage by hour of the day for each membership type?
<img width="500" alt="Rides by Hour of the Day" src="https://github.com/user-attachments/assets/3584f3d6-0c03-4f53-a0cb-7817b8e84c46"> <br>
Casual riders experience peak bike usage in the late afternoon to early evening, especially between 17:00 and 18:00, with 868,303 rides. Annual members, on the other hand, peak in the morning and early afternoon, with the highest number of rides at 17:00 (1,464,955). Both casual and annual members show similar patterns of low usage late at night, from 00:00 to 04:00. This suggests that while casual riders favor the late afternoon and evening, annual members use bikes more during typical commuting hours.

#### 4.1.5. What are the top 10 most frequent routes taken by each membership type?
<img width="500" alt="Top 10 Most Frequent Routes" src="https://github.com/user-attachments/assets/d01896da-35d6-42b1-bdde-a914cf881af6"> <br>
Casual riders frequently travel to popular city locations such as DuSable Lake Shore Dr & Monroe St and Millennium Park. Annual members, however, often take routes like Ellis Ave & 60th St and University Ave & 57th St. This indicates that casual riders are more likely to visit notable city destinations, while annual members’ routes are more indicative of regular commuting or specific destinations.

#### 4.1.6. How do rideable type preferences vary by time of day and membership type?**
<img width="1000" alt="Preference Bike Type" src="https://github.com/user-attachments/assets/e8c23041-a5e6-4702-979b-7b308c4cd570">
 <br>
Casual riders prefer electric bikes, with peak usage occurring between 12:00 and 18:00, aligning with midday to early evening activities. In contrast, annual members favor classic bikes, especially during the morning and early afternoon hours, likely reflecting their use for regular commutes.

#### 4.1.7. What are the popular ride duration segments for each membership type?
For casual riders, the most popular ride duration segments are medium (3,634,730 rides) and long (2,396,451 rides) rides. Annual members prefer medium (6,891,259 rides) and short (3,139,432 rides) rides. This indicates that casual riders are inclined towards longer rides, while annual members favor shorter, more frequent trips.

#### 4.1.8. What are the popular start times for casual riders on weekends?
Casual riders predominantly start their rides between 13:00 and 15:00 on weekends, with the peak start time at 15:00 (310,933 rides). This suggests that the early to mid-afternoon is a popular time for casual riders to begin their rides on weekends.

#### 4.1.9. How do casual riders use specific rideable types?
Casual riders primarily use electric bikes, accounting for 3,939,580 rides, followed by classic bikes (3,428,739 rides) and docked bikes (1,703,804 rides). Electric bikes are the most popular among casual riders.

#### 4.1.10. What are the most common start and end stations for casual riders?
Casual riders frequently use stations such as Streeter Dr & Grand Ave, Michigan Ave & Oak St, and DuSable Lake Shore Dr & Monroe St. The most popular start and end station is Streeter Dr & Grand Ave, with 40,196 rides. Other notable stations include Michigan Ave & Oak St (19,954 rides) and DuSable Lake Shore Dr & Monroe St (19,823 rides). Casual riders also frequently visit Millennium Park, Buckingham Fountain, and Theater on the Lake, among others.

#### 4.2.11. How frequently do casual riders use bikes during commuting hours?
Casual riders are active during peak commuting hours, with significant usage recorded at 7:00 (192,003 rides), 8:00 (261,577 rides), 9:00 (285,530 rides), 16:00 (780,419 rides), 17:00 (868,303 rides), and 18:00 (770,277 rides). This shows a strong presence during both the morning and evening commuting periods.

### 4.2. Summary
- **Usage Patterns**: Annual members ride more frequently and prefer shorter trips, while casual riders take longer rides and are more active on weekends.
- **Ride Preferences**: Casual riders use bikes mainly in the late afternoon and visit popular city locations. Annual members ride more during weekdays and stick to regular commuting routes. Both groups prefer electric bikes, but at different times.
- **Membership Motivation**: Casual riders frequently use popular stations and are active during peak commuting hours. Highlighting the convenience and savings of membership at these stations and times can be effective. Personalized offers and targeted promotions can address casual riders' specific needs and preferences.

## 5. Recommendations

1. **Highlight Usage Trends**: Focus campaigns on peak times and popular routes for casual riders. Target late afternoons to early evenings when casual riders are most active. Use metrics like click-through rates and engagement levels to gauge campaign success.
2. **Promote Convenience and Savings**: Emphasize how memberships provide easier access to popular stations and offer savings during peak commuting hours. Highlight the benefits of membership for high-demand stations and times, and use feedback from new members to refine these messages.
3. **Customize Offers**: Develop personalized promotions based on casual riders' preferences, such as frequent use of electric bikes or popular start times. Showcase how memberships fit their ride habits to make the transition more attractive. Utilize social media, email campaigns, and local partnerships to reach target audiences effectively.
