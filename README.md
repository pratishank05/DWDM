# partsUnlimitedDW - Data-Warehouse-Project

## Background information 
The topic I wish to explore for my data warehouse project is the management of Parts Unlimited's EV parts business, inspired by the book "The Unicorn Project"(Auther: Gene Kim).  This project aims to improve the organization's data management, reporting, and analysis capabilities related to its existing EV parts business.

## Files Included:
* data folder: Inculudes csv files and pdf files for the data warehouse from the different data source (please project documents folder for more information about the data sets)
* figures and images folder: the images and figures used in the documenatain of the project.
* project documents folder: inculudes project presentation, project research document and ipynb file. 
* elt files: please see etl process of each fact tables
queries file :Using sql queries to respond business questions.
* scd maintance file: this file provides information and example of how to maintain datawarehouse dimention tables keys and scd maintance. 

## Project Summary:
The primary objective of this project was to create a concept data warehouse project using a slowly changing dimension approach. I identified the business requirements and developed a consolidated ERD schema for the data warehouse, focusing on storing and analyzing data related to EV charging stations, product information, customer purchases, and geographic location.

To ensure data was properly tracked over time, I used a slowly changing dimension approach with SCD Type 2 to track changes to the customer's location, SCD Type 3 to track changes to the EV product information, and SCD Type 1 to track changes to the charging station information.

Finally, I used Tableau and Postgres SQL to create reports that helped the business make data-driven decisions based on the data stored in the data warehouse. This ensured that the data warehouse accurately reflected the business needs and provided valuable insights to the organization.

## Business Questions:
1. What is the distribution of EV charging stations and EV cars across different geographic regions, and how does this relate to the popularity of EVs in those regions? 
2. How has the popularity of different EV models and electric vehicle types varied by geographic region over time, and how can Parts Unlimited use this information to target their marketing and sales efforts more effectively?
3. How does the weight of EV parts relate to their price, and how does this relationship differ across different manufacturers?
4. What is the average price, weight, and quantity of products sold by Parts Unlimited over time, and how does this vary across different geographic regions in which the products have been manufactured?
5. How do the demand for charging stations and the number of vendors operating in different regions relate to the size of the EV market? What trend can be identified over time? 

## Design schema for the data warehouse:
![alt text](images/erd.png "Optional title")

## Dimensions:
Based on the business requirements, I have incorporated a Manufacturer dimension table to monitor PartsUnlimited's manufacturer information, as well as a Products table to keep track of the manufacturer's products. To track location and time information of these dimensions and streamline the design, I have also employed the use of Location and Date dimensions, with the Location dimension serving as a role-playing dimension. 

In addition, I have created EV_Population and EV_Charging_Stations dimensions to track information about the electric car population and charging stations for the research part of the project.

To tie all of these dimensions together, I have created a cumulative fact table that summarizes data across all dimensions. The Month dimension was created as a different time grain dimension to allow for easy aggregation of data by month. By including all relevant dimensions in the fact table, we can generate meaningful insights and answer business questions with ease.

## Fact Tables:
I have included three fact tables in the design. The first two are snapshot fact tables - one for the operational part, which is the Manufacturer Fact Table, and the other one is the Charging Stations Fact Table. These tables track detailed information for a specific time period.

To connect and summarize data across all dimensions, I have also created a Cumulative Fact Table. This table helps optimize query run time and provide insights by summarizing data across all dimensions.

## ETL:
While finding EV parts data was challenging, it provided an opportunity to learn. Initially, I extracted EV parts information from the evparts.com website as a PDF. Later, I developed an algorithm to extract EV parts, prices, and manufacturer information from these PDF documents. More information about the data can be found in the project documents folder.

Using Python's Pandas library, I transformed and cleaned the data according to the business questions and my ERD schema. Pandas helped speed up the process, as it is particularly good at data cleaning and transformation.

Finally, I used SQL to create the tables and loaded the data using Pandas' `to_sql` function with the append parameter.

## Maintaining SCD types- Delta Loads:
 During the initial creation of the dimension tables, I realized I forgot to implement the primary key (PK) and surrogate key (SK) fields to increase automatically. I realized that when I was working on delta loads. To remedy this, I used an ALTER CREATE SEQUENCE statement to add the PK and SK keys to the tables to increase atumatically. I also used another ALTER statement to set the slowly changing dimension (SCD) fields to default values.

This process presented some challenges, and I learned that it's essential to set default values for SCD fields and configure automatic PK and SK increments. This would enable me to load data without worrying about these fields. Please see more information about the scd and key maintenance ipynb file.

## Querying and visualization: 
I used sql to create my queries for the business questions and tableau to visualize it. PLease see project presentation and queries ipynb file for more information.

## Conculation:
In conclusion, this project taught me the importance of designing a system that is flexible and adaptable over time. Creating and implementing such a system requires a strong vision and careful planning to anticipate potential changes based on current information. One of the challenges I faced during this project was connecting the datasets, as one part was related to operations and the other to research at PartsUnlimited. Finding a common field to connect the data was difficult, but I was able to merge the two fields by connecting them with cumulative fact tables. This enabled me to summarize the operations and research data together. Learning how to identify useful information and connect it to existing data is a challenge that must be overcome, and I am grateful for the experience gained through this project.

I also learned firsthand that a well-implemented database can reduce the time and effort required to access and query data. Working on my queries and visualizing them helped me appreciate the benefits of a good database design.

## updated at 
05/2023

