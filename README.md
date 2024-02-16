# Uber-Data-Analytics-End-To-End-Data-Engineering-Project
Using an Uber dataset, I will build a data model in fact and dimension format and write the transformation code in Python. This code will then be deployed on a compute instance on Google Cloud, where Mage will be installed. We will then load our data onto big query which is in data warehouse and create our final dashboard.
## Architecture
![architecture](https://github.com/Areefkk/Uber-Data-Analytics-End-To-End-Data-Engineering-Project/assets/36210165/1219d4f2-6dea-4aad-a668-34a52f8f9d24)
## Google Cloud Platform (GCP) Services
### Cloud Storage
Google Cloud Storage is an online file storage service provided by Google as part of its cloud computing platform. It allows you to store and retrieve your data in the cloud, making it accessible from anywhere with an internet connection.
### Compute Engine
Google Compute Enginer is a cloud computing service that provides virtual machines for running applications and services. It allows you to easily create, configure and manage virtual machines with various operating systems and hardware configurations.
### BigQuery
Bigquery is cloud-based data warehouse provided by Google Cloud Platform that allows you to store, analyse, and query large datasets using SQL-like syntax. It is a serverless, highly scalable, and cost-effective solution that can process and analyse terabytes to petabytes of data in real-time.
### Looker
Looker Studio is a web-based data visualization and reporting tool that allows you to create interactive dashboards and reports from various data sources, including Google Analytics, Google Sheets, and BigQuery. It enables you to turn your data into informative and engaging visualisations, which can be easily shared and collaborated on with others.
## Dataset Used
TLC Trip Record Data
Yellow and green taxi trip records include fields capturing pick-up and drop-off dates/times, pick-up and drop-off locations, trip distances, itemized fares, rate types, payment types, and driver-reported passenger counts.

More info about dataset can be found here:
1. Website - https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page
2. Data Dictionary - https://www.nyc.gov/assets/tlc/downloads/pdf/data_dictionary_trip_records_yellow.pdf
## Data Model
![data_model](https://github.com/Areefkk/Uber-Data-Analytics-End-To-End-Data-Engineering-Project/assets/36210165/276d1181-d37e-4141-9637-4bda83f87925)

## Step 1: Creating Fact & Dimension Table

Fact Table:
- Contains the quantitative measures or metrics used for analysis
- Typically contains foreign keys that link to dimension tables
- Contains columns that have high cardinality and change frequently  
- Contains columns that are not useful for analysis by themselves, but are necessary for metric calculation

Dimension Table:
- Contains columns that describe attributes of the data being analysed
- Typically contains primary keys that link to fact tables
- Contains columns that have low cardinality and do not change frequently
- Contains columns that can be used for grouping or filtering data for analysis

Jupyter Notebook (pandas) and the data csv file:


Change Pickup_datetime and dropoff_datetime rom object data type to datetime type. This allows extraction of information from the data.

![1](https://github.com/Areefkk/Uber-Data-Analytics-End-To-End-Data-Engineering-Project/assets/36210165/e82bd8a0-b593-4902-9af2-6ae9be03a0a5)

Using the data model, reset the index and drop the duplicates. Then extract the required hour, day, month, year, weekday and assign to the new columns created for pick hour, pick day, pick month, etc.

Order the data into the correct format ensuring the correct primary key.

For all required data in the data model, drop dupliclicates, reset the index, assign the index to the required ID column and reorder the information as per the data dimension model.


![2](https://github.com/Areefkk/Uber-Data-Analytics-End-To-End-Data-Engineering-Project/assets/36210165/e868045a-834d-4dbc-b682-a40267beb03d)


For ratecodeID, we require the rate_code_name which is not in the data frame.
Therefore, create a data dictionary, drop the duplicates, reset the index, and assign the index to ratecodeID. Use the rate_code_name and map to the ID so the value is assigned to the standard rate. Finally reorder as per the data model.

![4](https://github.com/Areefkk/Uber-Data-Analytics-End-To-End-Data-Engineering-Project/assets/36210165/e827dab6-cee2-47f4-adc4-8831fcb5b59a)


Now that all Dimension Tables created, create the Fact Table by joining the dimension tables based on the common columns between the tables.

![3](https://github.com/Areefkk/Uber-Data-Analytics-End-To-End-Data-Engineering-Project/assets/36210165/9c393628-76b1-4530-8c4f-3d94c1b73286)

