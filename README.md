Data Analytics Framework for MOT Data

 
 
# Abstract 

This project aims to build a data pipeline framework and analyze passenger vehicle inspection data. In this project, an exploratory analysis of the MOT test vehicle results dataset is conducted to discover patterns and spot anomalies. Using the transformed data,  a dashboard is built using Google Data Studio to know about the test results, test outcomes, pass and fail vehicles, and the fuel types of the vehicle.

# Keywords 

Roadworthiness, Data Analytics, Vehicle Technical Inspection, Mechanical failures

# I. INTRODUCTION

The evolution of the automotive sector in the wake of the surge in demand for automobiles for business and private objectives promotes the necessity to monitor the technical state of these automobiles, which helps to ensure their safe operation. It is a fact that automobiles that are in good technical condition perform their task at a high level and promotes road safety.

The vehicles over a prescribed age need to be inspected at least once a year to view that they follow basic requirements in terms of roadworthiness and environmental demands. Roadworthiness is the ability of automobiles to be in a satisfactory operating state for safe transport on roads. Many countries have undertaken different measures related to roadworthiness that aimed at improving road safety through periodic tests for automobiles. An automobile is deemed ‘roadworthy’ if there are no minor defects when the technical assessment is implemented. An automobile is considered to be ‘temporarily roadworthy’ if one major defect is spotted and no dangerous defect is noticed when the inspection is implemented to a certain degree. If at least one dangerous defect is spotted, it is considered ‘not roadworthy’.

The roadworthiness test conducted in the UK is known as the Ministry of Transport (MOT) test.  The assessment is compulsory by law for any vehicle registered in the United Kingdom that is over 3 years old. Upon completion, test certificates are issued. In the year 2005 the Department for Transport, UK published the MOT data. It consists of two datasets known as testing data results and failure item results. 

The proposed framework consists of the processes starting from acquiring the MOT datasets from its source, changing file formats, conducting transformations, and then storing the data in the data warehouse, the analytics used to extract insights, and lastly creating a dashboard to present extracted insights to the user. 

The key goals are:

 - Create a data pipeline that will help to organize data processing.
 - Conduct exploratory data analysis on the dataset.
 - Build an analytical dashboard to help users discover trends and insights.
   
The rest is structured as follows: Section II presents the related work. Section III explores the dataset. Section IV describes the framework architecture. Section V and VI explains the exploratory data analysis and the dashboard. Section VII outlines the conclusion.

# II. RELATED WORK

The roadworthiness inspection test is done periodically and the generated data is used for different purposes. Hudec et al. [1] investigated the evaluation of the technical state of automobiles at the stations where periodic inspections are conducted in a few European nations in a particular year and compared it with the average age of the automobiles. It was found that the results of the evaluation of each state differ and do not depend on the age of the automobile.

Zulkipli et al. [2] explored taxi roadworthiness periodic inspection data. Descriptive analysis was conducted to identify the trends and a logistic regression model was developed for failure concerning the vehicle age. Based on the results, recommendations were proposed and it was concluded that the poorly maintained taxi was more likely to fail the periodic inspection than the well-maintained one.

Emmerson et al. [3] explored the MOT dataset and investigated spatial patterns of vehicle ownership, its characteristics like age, size, and its uses in Scotland. The authors compared the spatial pattern of mileage per car with patterns from a traditional transport model. Spatial patterns of emissions mainly CO_2 and NO_2 were also compared. Tarancón-Andrés et al. The authors in [4] also analyzed the potential consequence of vehicle roadworthiness tests on the minimization of impacts on environmental issues due to emissions from agricultural vehicles in a community in Spain.

Hudec and Šarkan [5] examined the relationship between periodic technical inspection and traffic accidents because of technical defects in automobiles in the Slovak Republic. It was found that the probability of accidents on account of technical faults elevates for vehicles. It was also found that the vehicle technical defects dropped due to the assessment of the vehicles at Periodical Technical Inspection stations. Correlation and regression analysis were used for the purpose. The results concluded that inspection affects accidents caused by defects. Reyes et al. [6] evaluated different literature surveys related to the effect of automobile roadworthiness inspections and road accidents. The authors deduced that the inspections are linked with road accidents and there is a modest reduction in accidents.

Narváez-Villa et al. [7] proposed models for analyzing and predicting the mileage (in kilometers) of vehicles based on technical inspection data. The information resulting from the analysis can be helpful in revising policies and regulations in the domain of road welfare.

Alonso et al. [8] analyzed vehicle technical inspection data and the vehicle driver’s perspectives toward the inspection with the level of compliance in Spain. It was found that the majority of drivers go along with the inspections but the dominant reason was to avoid fines and sanctions.

From the above papers, it can be seen that vehicle inspection data can be used and explored for different purposes. It can be also used for gaining insights into vehicle ownership, and vehicle reliability, and even for providing purchase recommendations to users.

# III. DATASET

Vehicle test result contains detailed documentation about the dates, area, and end result of the MOT inspection in addition to the details about the vehicle tested as shown in Table 1. Vehicle test item contains  details of individual MOT test failure items and the reason for rejection (Table 2).

For this, only the vehicle test result dataset will be used for exploratory analysis and build a dashboard according to it.

Column Name	Description
Test ID	Unique Identifier for a test
Vehicle ID	Unique Identifier for a vehicle
Test Date	Date of Test
Test Class ID	Class of Vehicle Tested
Test Type	Type of M.O.T. Test
Test Result	Test Outcome
Test Mileage	Mileage recorded at the point of test
Postcode Area	Test Location
Make	Vehicle Make
Model	Vehicle Model
Color	Vehicle Colour
Fuel Type	Vehicle Fuel Type
Cylinder Capacity	Vehicle Cylinder Capacity
First use Date	Vehicle Date of First Use
Table 1. Test Vehicle Result
Column Name	Description
Test ID	Unique Identifier for a test
RfR ID	Reason for Rejection ID
RfR Type	Reason for Rejection Type
Location ID	Failure Location ID
D Mark	Dangerous Item Marker
Table 2. Vehicle test item

# IV.  ARCHITECTURE

The framework consists of a group of components as shown in Fig1. They are as follows:

1. Terraform
   
It is an open-source infrastructure as a code (IaC) tool developed by HashiCorp. It is a cloud infrastructure provisioning and managing tool written in the Go language [9]. This paper uses terraform to build and manage the GCP infrastructure.

2. Google Cloud Platform (GCP):
   
It provides a suite of cloud computing services. In this paper, we used the following GCP products:
- Google Cloud Storage: 
    A data lake provides a scalable and secure platform to ingest and store large amounts of data ignoring size limits. Google Cloud Storage can store any amount of data and retrieve it as often as required. It is chosen due to its strong consistency, performance, and 
    flexible processing.
- BigQuery: 
    A completely serverless and cost-effective enterprise data warehouse. It uses SQL and focuses on analyzing data to find meaningful insights.
    
3. Docker:
   
It is an open platform for fast developing, testing, and deploying applications. It delivers software in packages known as containers. The docker container is an isolated environment that includes applications and all their dependencies. Docker is used in this project, to encapsulate package dependencies the code may have, which allows the code to run any data. Docker is used in this project to deploy Apache Airflow.

4. Airflow:
   
It is an open-source platform for developing, scheduling, and monitoring batch-oriented workflows [10]. It is used as a tool for the orchestration of pipelines/workflows due to its dynamic, extensible, and flexible behavior. It allows tasks to be defined in a Directed Acyclic Graph (DAG) with dependencies allowing the tasks to be optimized. In case of failure in any part of the pipeline, it allows users to check the steps. This project uses Airflow to build an automated data pipeline. The workflow is shown in Fig2.

5. Google Data Studio
   
Also known as Looker Studio, it is a free reporting and visualization tool. Widgets include pie charts, heat graphs, and many more. It can also pull data from multiple sources. It allows us to connect, visualize and share reports.

 ![image](https://github.com/user-attachments/assets/4ac9e175-5998-4476-a597-360e0c048af3)

 
 <div align="center"> Fig 1: Architecture diagram </div>    

![image](https://github.com/user-attachments/assets/a3ca9f48-8d1e-4301-8b6a-a9699148daa9)

<div align="center">Fig 2: Airflow workflow</div> 

 
The framework includes the following steps:

1. First, set up the docker, terraform, and Google Cloud Platform in the host system
2. And then host the airflow in the docker
3. MOT dataset files (CSV) are downloaded from data.gov.uk. using the wget command.
4. It is extracted, cleaned, and then converted to parquet files by using python operator.
5. Parquet dataset files are uploaded to the data lake i.e., the Google Cloud Storage.
6. Data tables for the 2 data sets are created in the data warehouse i.e., the Google BigQuery, and are populated with the data from the parquet files in the data lake.
7. Exploratory analysis is conducted using python libraries on the data from BigQuery.
8. After the data is transformed and ready, it is again loaded in the BigQuery
9. A new table is created for performing the analysis by using a query shown in Fig 3.
10. Lastly, a dashboard is built using Google Data Studio for displaying the analysis.

 ![image](https://github.com/user-attachments/assets/c02f2287-3078-45e9-8b87-2d260a56629f)

<div align="center"> Fig 3: Query for creating a table</div>


# V. EXPLORATORY DATA ANALYSIS

The MOT data loaded in the BigQuery is extracted for performing an exploratory analysis using python libraries. Two types of analysis are done. They are as follows:

## 1. Univariate Analysis
 
Here, the distribution of individual variables is reviewed and summary statistics is generated. This will give us an idea of the distribution of the data and help identify any outliers or unusual observations.

First, the test_class_id is changed to string as a mathematical operation cannot be performed in this data.

![image](https://github.com/user-attachments/assets/19748ee7-f67b-4e61-8d79-651fd196b2a7)

<div align="center"> Fig 4: Change datatype</div>

There are no missing values in all the columns in the data as seen in Fig 5.

![image](https://github.com/user-attachments/assets/f5220289-274b-4237-a3b1-f02b1da1d331)

<div align="center"> Fig 5: Checking missing values</div>

To understand the variations in the data, summarized the statistics of test mileage and cylinder capacity.

![image](https://github.com/user-attachments/assets/67a49b49-8ca4-41f0-8c94-80fb8eefdc8c)

<div align="center"> Fig 6: Summary statistics</div>

Fig 6. presents summary statistics for two columns in a Pandas DataFrame named df: test_mileage and cylinder_capacity. These statistics provide insights into the central tendencies, dispersion, and ranges of the data within these columns.

Breakdown of Statistics:

- count: The number of non-null values in each column. Both test_mileage and cylinder_capacity have 39,981,930 non-missing values.
- mean: The average value for each column. The mean test_mileage is 74,189.03, and the mean cylinder_capacity is 1,711.46.
- std: The standard deviation, measuring the amount of variation or dispersion from the mean. The standard deviation for test_mileage is 48,664.85, and for cylinder_capacity is 604.9965.
- min: The minimum value in each column. The minimum test_mileage is 1, and the minimum cylinder_capacity is 0.
- 25%: The first quartile (Q1), representing the value below which 25% of the data falls. Q1 for test_mileage is 37,681, and for cylinder_capacity is 1,349.
- 50%: The median (Q2), representing the middle value of the dataset when sorted. The median test_mileage is 65,723, and the median cylinder_capacity is 1,598.
- 75%: The third quartile (Q3), representing the value below which 75% of the data falls. Q3 for test_mileage is 100,839, and for cylinder_capacity is 1,995.
- max: The maximum value in each column. The maximum test_mileage is 999,999, and the maximum cylinder_capacity is 99,999.

The following can be interpreted from the plot:
- Test Mileage: The test_mileage data appears to be right-skewed, with a mean higher than the median and a significant difference between the third quartile and the maximum value. This suggests the presence of some high-mileage outliers.
- Cylinder Capacity: The cylinder_capacity data also seems to be right-skewed, with a mean higher than the median and a larger gap between the third quartile and the maximum value. This indicates the presence of some vehicles with much larger cylinder capacities.

Further Analysis can be executed to gain a deeper understanding of the data, it would be beneficial to:
- Visualize the distributions using histograms or box plots to identify potential outliers and the shape of the distributions.
- Explore the relationship between test_mileage and cylinder_capacity through scatter plots or correlation analysis.

![image](https://github.com/user-attachments/assets/271dcd23-ad83-4608-8fdb-9a2cd061c220)

<div align="center"> Fig 7: Outliers</div>

Using a scatter plot, outliers can be seen in the cylinder capacity, data as shown in Fig 7. The scatter plot illustrates the relationship between a vehicle's cylinder capacity and its test mileage. Each dot represents a data point, with its position indicating the specific values for cylinder capacity and test mileage.

The following observations can be seen from the plot:
- Density Distribution: The plot shows a clear density distribution, with a higher concentration of data points towards the lower end of both cylinder capacity and test mileage. This suggests that a larger proportion of vehicles in the dataset have smaller engines and lower mileage readings.
- Positive Correlation: While not as pronounced as in some scatter plots, there seems to be a slight positive correlation between cylinder capacity and test mileage. This indicates that, generally, vehicles with larger engines tend to have higher mileage values, although there are exceptions.
- Outliers: A few data points deviate significantly from the main cluster. These could represent vehicles with exceptional characteristics, measurement errors, or other anomalies.

The following can be the possible interpretations from the plot:
- Engine Size and Mileage: The plot hints at a potential relationship between engine size (cylinder capacity) and the total distance a vehicle has traveled (test mileage). Larger engines might be associated with vehicles that are driven more frequently or for longer distances.
- Vehicle Types: The data distribution could reflect different vehicle types within the dataset. Smaller, more fuel-efficient cars might dominate the lower left corner, while larger, less fuel-efficient vehicles could be positioned towards the upper right.
- Other Factors: Factors beyond engine size and mileage, such as vehicle age, driving conditions, and maintenance history, could influence the data distribution.

In order to gain deeper insights, futher analysis can be executed such as:
- Correlation Coefficient: Calculate the correlation coefficient to quantify the strength of the relationship between cylinder capacity and test mileage.
- Data Segmentation: Explore the data by vehicle type, age, or other relevant categories to identify potential patterns within specific groups.
- Additional Visualizations: Create histograms or box plots for cylinder capacity and test mileage to understand their distributions independently.
  
Overall, the scatter plot provides a preliminary overview of the relationship between cylinder capacity and test mileage. Further analysis is necessary to draw more definitive conclusions and uncover underlying trends.

## 2. Bivariate Analysis

Here, the relationship between different variables is observed.

 ![image](https://github.com/user-attachments/assets/f3660642-4521-459c-a38f-939a8826bf6f)

The above plot visualizes the relationship between "Cylinder Capacity" and "Test Mileage" for a dataset. Each dot represents a data point, with its x-coordinate corresponding to the test mileage and its y-coordinate representing the cylinder capacity.

The following observations can be seen from the plot:
- Positive Correlation:There appears to be a weak to moderate positive correlation between cylinder capacity and test mileage. This means that as cylinder capacity increases, test mileage tends to increase as well, although the relationship is not very strong.
- Clustering:The data points exhibit some clustering, particularly around lower cylinder capacities and test mileages. This suggests that a certain segment of vehicles tends to have smaller engines and lower mileage.
- Outliers: There are a few outliers in the plot, notably data points with high cylinder capacities but relatively low test mileage. These might represent specific vehicle types or experimental data points that deviate from the general trend.

But limitations can be also be found such as:
- No Clear Trend: The correlation between the variables is not very strong, making it difficult to draw definitive conclusions about the relationship.
- Missing Context: Without additional information about the dataset (e.g., vehicle types, years, etc.), it's challenging to interpret the plot's meaning fully.

To gain deeper insights, the following can also be considered:
- Correlation Coefficient: Calculate the correlation coefficient to quantify the strength of the relationship between the variables.
- Data Segmentation: Analyze the data by vehicle type, year, or other relevant categories to identify potential patterns within specific groups.
- Other Plots: Explore additional visualizations like box plots or histograms to understand the distribution of cylinder capacities and test mileages separately.

In conclusion, while the plot suggests a possible link between cylinder capacity and test mileage, further analysis is also needed here to draw more robust conclusions.

![image](https://github.com/user-attachments/assets/f25045f7-20eb-43b5-9e96-5ef694382219)

<div align="center"> Fig 8: Correlation between cylinder capacity and mileage using different plots</div>

The scatter plot illustrates the relationship between a vehicle's cylinder capacity and its test mileage. Each dot represents a data point, with its position indicating the specific values for cylinder capacity and test mileage.
The following observations can be made,
- Density Distribution: The plot shows a clear density distribution, with a higher concentration of data points towards the lower end of both cylinder capacity and test mileage. This suggests that a larger proportion of vehicles in the dataset have smaller engines and lower mileage readings.
- Positive Correlation: While not as pronounced as in some scatter plots, there seems to be a slight positive correlation between cylinder capacity and test mileage. This indicates that, generally, vehicles with larger engines tend to have higher mileage values, although there are exceptions.
- Outliers:A few data points deviate significantly from the main cluster. These could represent vehicles with exceptional characteristics, measurement errors, or other anomalies.

the following possible interpretations can be as follows:
- Engine Size and Mileage: The plot hints at a potential relationship between engine size (cylinder capacity) and the total distance a vehicle has traveled (test mileage). Larger engines might be associated with vehicles that are driven more frequently or for longer distances.
- Vehicle Types: The data distribution could reflect different vehicle types within the dataset. Smaller, more fuel-efficient cars might dominate the lower left corner, while larger, less fuel-efficient vehicles could be positioned towards the upper right.
- Other Factors: Factors beyond engine size and mileage, such as vehicle age, driving conditions, and maintenance history, could influence the data distribution.

In order to gain deeper insights the following can be done:
- Correlation Coefficient: Calculate the correlation coefficient to quantify the strength of the relationship between cylinder capacity and test mileage.
- Data Segmentation: Explore the data by vehicle type, age, or other relevant categories to identify potential patterns within specific groups.
- Additional Visualizations:Create histograms or box plots for cylinder capacity and test mileage to understand their distributions independently.

Overall, the scatter plot provides a preliminary overview of the relationship between cylinder capacity and test mileage. 

# V. DASHBOARD

![image](https://github.com/user-attachments/assets/28f90133-4d49-4012-bfcb-832b75093154)

<div align="center"> Fig 9: Dashboard for MOT Passenger Vehicles Test</div>

The dashboard in Fig 9 is created using Google Data Studio (Looker Studio). The fig presents a dashboard summarizing various aspects of M.O.T. (Ministry of Transport) passenger vehicle tests conducted in 2021. It includes multiple charts and graphs to visualize key metrics. Here, seven charts are used to represent the findings. 
- Scorecard: It displays the total number of tests for passenger vehicles.
- Line chart: It displays the number of tests conducted in each month in the year 2021.
- Column chart: It displays the number of tests per day in a particular month.
- Bar graph: It represents the test results outcomes as shown in Table 3.
- Table: It displays the fuel types and the number of vehicles associated with it
- Heat Map: It displays the make of the passenger vehicles. We can see from the heatmap that the Ford is the most tested vehicle.
- Pie chart: It displays the models for every make which has done the MOT test.

Breakdown of Visualizations:
- Test Results Over Time: A line chart displaying the number of test results per month. Peaks and troughs indicate fluctuations in test volumes throughout the year.
- Fuel Types: A bar chart showing the distribution of test results across different fuel types. The length of each bar represents the number of tests for a specific fuel type.
- Make: A treemap visualizing the frequency of different vehicle makes in the test data. The size of each word or block corresponds to the number of vehicles of that make.
- Model: A pie chart illustrating the distribution of test results across different vehicle models. The size of each slice represents the percentage of tests for a particular model.
- Numerical values are displayed for total displayed tests (37.8M).

The following potential insights can be interpreted from the dashboard:
- Identify peak months for vehicle testing.
- Determine the most common fuel types for tested vehicles.
- Recognize popular vehicle makes and models.
- Analyze trends in test results over time (e.g., increasing or decreasing test volumes).
    
# VI. CONCLUSION

Periodic technical inspection is to ensure that road vehicles remain roadworthy and safe and do not pose danger to drivers or other road users. The data generated during these inspections are very useful for different purposes. So, a data pipeline framework is proposed using different technologies for processing MOT datasets. By performing exploratory analysis, summary statistics about variables is generated and even found outliers in the variables of the dataset. The dashboard created shows the number of tests of every month in a year for passenger vehicles, the types of fuels used by these vehicles, and the test outcomes of all the vehicles. Thus, the information gathered will be useful to know about reliable vehicles and will also be helpful to automakers.

# REFERENCES

[1]	J. Hudec, B. Šarkan, and R. Cződörová, “Examination of the results of the vehicles technical inspections in relation to the average age of vehicles in selected EU states,” Transportation Research Procedia, vol. 55, pp. 2–9, 2021, doi: 10.1016/j.trpro.2021.07.063.

[2]	Z. H. Zulkipli, R. Sarani, A. N. S. Zainal Abidin, M. S. Solah, and M. R. Osman, “Periodical Technical Inspection on Taxi Roadworthiness,” Journal of the Society of Automotive Engineers Malaysia, vol. 3, no. 4, pp. 41–47, Apr. 2021, doi: 10.56381/jsaem.v3i4.138.

[3]	P Emmerson, J Anable, T Chatterton, S Cairns, E Wilson, and S Ball, “Analysing MOT vehicle licensing data and transport model data to generate insights about car use and emissions in Strathclyde,” in Scottish Transport Applications & Research (STAR) conference, 2016.

[4]	E. Tarancón-Andrés, J. Santamaria-Peña, D. Arancón-Pérez, E. Martínez-Cámara, and J. Blanco-Fernández, “Technical Inspections of Agricultural Machinery and Their Influence on Environmental Impact,” Agronomy, vol. 12, no. 4, p. 907, Apr. 2022, doi: 10.3390/agronomy12040907.

[5]	J. Hudec and B. Šarkan, “Effect of Periodic Technical Inspections of Vehicles on Traffic Accidents in the Slovak Republic,” Communications - Scientific letters of the University of Zilina, vol. 24, no. 3, pp. A142–A159, Jul. 2022, doi: 10.26552/com.C.2022.3.A142-A159.

[6]	L. M. Martín-delosReyes, P. Lardelli-Claret, L. García-Cuerva, M. Rivera-Izquierdo, E. Jiménez-Mejías, and V. Martínez-Ruiz, “Effect of Periodic Vehicle Inspection on Road Crashes and Injuries: A Systematic Review,” Int J Environ Res Public Health, vol. 18, no. 12, p. 6476, Jun. 2021, doi: 10.3390/ijerph18126476.

[7]	P. Narváez-Villa, B. Arenas-Ramírez, J. Mira, and F. Aparicio-Izquierdo, “Analysis and Prediction of Vehicle Kilometers Traveled: A Case Study in Spain,” Int J Environ Res Public Health, vol. 18, no. 16, p. 8327, Aug. 2021, doi: 10.3390/ijerph18168327.

[8]	F. Alonso, S. A. Useche, J. Gene-Morales, and C. Esteban, “Compliance, practices, and attitudes towards VTIs (Vehicle Technical Inspections) in Spain: What prevents Spanish drivers from checking up their cars?,” PLoS One, vol. 16, no. 7, p. e0254823, Jul. 2021, doi: 10.1371/journal.pone.0254823.

[9]	Terraform by HashiCorp. [Online]. Available: https://www.terraform.io/

[10]	Apache Airflow. [Online]. Available: https://airflow.apache.org/docs/apache-airflow/stable/index.html 

