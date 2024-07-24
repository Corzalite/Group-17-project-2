# README: Group-17-project-2

This README is for Project 2 - Crowdfunding ETL of the Data Bootcamp April Session.

[![License](https://github.com/Corzalite/Group-17-project-2/blob/main/LICENSE)

## Table of contents

* [Introduction](#introduction)
* [Installation](#installation)
* [Extraction](#extraction)
* [Transformation](#transformation)
* [Load](#load)
* [Data Analysis](#data-analysis)
* [Question 1](#question-1)
* [Question 2](#question-2)
* [Question 3](#question-3)


## Introduction

What is ETL? ETL is the process of extracting, transforming, and loading data from multiples sources into a single central data repository. This is the process of taking raw data, cleaning and organizing the information into a usable format, and then loading it into a data repository. We can then access the data to improve business intelligence, generating analytics and reporting to better steer company decisions. This project is a showcase of the ETL process, culminating in an analysis of the data using SQL queries and data visualizations.

## Installation

Planning for the table structure of this project was done with [QuickDBD](https://www.quickdatabasediagrams.com/). Scripting for the ETL process and Data Analysis was done using [Anaconda](https://www.anaconda.com/download). We used an Anaconda Prompt to launch Jupyter Notebook, where our scripting was created. Our database and tables were created using [Postgres](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads).

## Extraction

In the Extraction phase, we were given raw data in the form of two excel files found in the [Resources](https://github.com/Corzalite/Group-17-project-2/tree/main/Resources) folder, to simulate retrieval of raw data from multiple sources. Each was saved in a different format for us to extract data into usable files for uploading into our database. 

The first, was [crowdfunding.xlsx](https://github.com/Corzalite/Group-17-project-2/blob/main/Resources/crowdfunding.xlsx).

This excel format had information clearly separated by columns. We were to use this file to separate information needed to generate our category, subcategory, and campaign tables. Our contacts table would require the second resource file, saved in JSON format.

The second, was [contacts.xlsx](https://github.com/Corzalite/Group-17-project-2/blob/main/Resources/contacts.xlsx).

## Transformation

After receiving our extracted data, we then transitioned into the Transformation phase. To begin this phase, we designed a table schema for our database using QuickDBD.  As part of this creation, we generated an [Entity Relationship Diagram](https://github.com/Corzalite/Group-17-project-2/blob/main/QuickDBD/QuickDBD-Project%202.png) to isolate necessary information for each required table and a [SQL Source File](https://github.com/Corzalite/Group-17-project-2/blob/main/QuickDBD/QuickDBD-Project%202.sql) for the scripting necessary to create tables within our database software, Postgres.

The next step in our Transformation phase was data cleaning and separation. To do this, we used Jupiter Notebook. All of our transformation scripting was done in [ETL_Mini_Project_Starter_Code.ipynb](https://github.com/Corzalite/Group-17-project-2/blob/main/ETL_Mini_Project_Starter_Code.ipynb). We used this notebook to transform the raw data into four CSV (comma-separated values) files that we would later use to load data into our Postgres tables.

For the category and subcategory tables, we split the “category & sub-category“ column into two columns, created an ID column, created DataFrames for each table, and exported the DataFrames as CSVs. 

[category CSV](https://github.com/Corzalite/Group-17-project-2/blob/main/CSV/category.csv)
[subcategory CSV](https://github.com/Corzalite/Group-17-project-2/blob/main/CSV/subcategory.csv)

For the campaign table, we renamed columns to more readable titles, changed datatypes, merged with the category and subcategory tables to bring in category_id and subcategory_id, dropped unwanted columns, and exported to a CSV.

[campaign CSV](https://github.com/Corzalite/Group-17-project-2/blob/main/CSV/campaign.csv)

For the contacts table, appended each row to a dictionary, created a DataFrame, split the name column into first and last name, reordered columns, an exported to a CSV.

[contacts CSV](https://github.com/Corzalite/Group-17-project-2/blob/main/CSV/contacts.csv)

Created CSVs stored in [CSV folder](https://github.com/Corzalite/Group-17-project-2/tree/main/CSV)

## Load

The final phase of the ETL process was the Load phase. The first step in our Load phase was to create a database, labelled project_two_etl, for the project within Postgres and use the [SQL script](https://github.com/Corzalite/Group-17-project-2/blob/main/QuickDBD/QuickDBD-Project%202.sql) created by QUICKDBD to create our four tables within that database. After the database and tables were generated, we created a second Jupyter Notebook, [ETL_Load CSVs](https://www.quickdatabasediagrams.com/), to house all of the script necessary to upload the CSVs to the Postgres tables. 

## Data Analysis

As a ship cannot steer without a rudder, companies cannot function effectively without data analytics. Our ETL pipeline supplied us with information about crowdfunding projects. Stopping there would be a disservice to the information we worked so hard to gather. Our group decided to review this information based on a West vs. East approach, using the United States (US) and Canada (CA) as the West and identifying the East as China (CH) and Australia (AU).

We separated our analysis into three questions:

1.	When grouped by category, how does the overall count of successes vs. failures differ for each of our four selected countries?
2.	How do our selected countries compare when looking at set goals, pledged finances, and number of backers?
3.	How does the length of a campaign compare to the success/failure of our selected countries?

To connect our Jupyter Notebook to our Postgres database. We set up an engine to communicate with our database and then inspected the engine to ensure communication. 

## Question 1

When grouped by category, how does the overall count of successes vs. failures differ for each of our four selected countries?

[success_vs_failure_combined.png](https://github.com/Corzalite/Group-17-project-2/blob/main/Charts/success_vs_failure_combined.png)

This dataset had a strong representation of US crowdfunding projects and a smaller number of overall projects for each of our other selected countries. We are able to see some interesting trends however. Three categories, film & video, music, and theater, had a strong representation in all four countries, showing a popularity for the arts in crowdfunding projects seeking support. It was also interesting to see four categories in China had more failures than successes, a trend that wasn’t reflected in the other three countries, leading us to believe projects in the west had a greater chance of success than in the east.

Individual query and charting work done in [Ind Nick Work/ETL_Data_Viz](https://github.com/Corzalite/Group-17-project-2/blob/main/Ind%20Nick%20Work/ETL_Data_Viz.ipynb). All required charting saved in [Charts](https://github.com/Corzalite/Group-17-project-2/tree/main/Charts) folder. 

## Question 2

How do our selected countries compare when looking at set goals, pledged finances, and number of backers?

The provided charts indicate a strong positive correlation between the funding goals and the pledged amounts, especially for successful projects, highlighting the importance of setting achievable and realistic goals. Higher backer counts generally lead to higher pledged amounts, emphasizing the need to engage and attract more backers for a successful campaign. The United States stands out as the dominant contributor, with significantly higher percentages of both backers and pledged amounts compared to other countries. Overall, while successful projects show consistent trends with high pledges and backer counts, failed and canceled projects exhibit more variability and inconsistency, underscoring the challenges in meeting high funding goals without sufficient support.

[East vs West Regression.png](https://github.com/Corzalite/Group-17-project-2/blob/main/Charts/East%20vs%20West%20Regression.png)

[East vs West, Success vs Failures.png](https://github.com/Corzalite/Group-17-project-2/blob/main/Charts/East%20vs%20West%2C%20Success%20vs%20Failures.png)

The scatter plots reveal that successful projects tend to have tighter distributions and higher concentrations of data points along the regression lines, suggesting a more predictable and stable relationship between goals and pledged amounts. In contrast, failed and canceled projects display a broader spread, indicating less predictability and greater challenges in reaching their funding targets. This variability underscores the importance of strategic planning and effective marketing to ensure sufficient backer engagement and support.

Additionally, the comparative analysis between different countries highlights significant disparities in contributions. The US, being a major player, shows a wide range of goals and pledged amounts, with larger backer counts correlating with higher pledges. Other countries like Canada, Australia, and China also contribute but to a lesser extent. These insights suggest that understanding and leveraging regional trends and backer behavior can be crucial for tailoring campaigns to maximize success. Overall, the data underscores the need for realistic goal-setting, robust backer engagement strategies, and awareness of regional dynamics to enhance the likelihood of successful crowdfunding campaigns.

The third chart reinforces the positive correlation between funding goals and pledged amounts across various countries and outcomes. Successful projects consistently show strong positive trends with higher pledges, especially in the US and Canada, indicating that well-planned campaigns significantly impact funding success. In contrast, failed and canceled projects display more variability, highlighting the difficulties in reaching funding targets without adequate support. The data emphasizes the importance of setting realistic goals, effectively engaging backers, and considering regional trends to tailor campaigns for maximum success.

[International scatter plot.png](https://github.com/Corzalite/Group-17-project-2/blob/main/Charts/International%20scatter%20plot.png)

Individual query and charting work done in [Ind Sam Work/Data_Viz_Sam](https://github.com/Corzalite/Group-17-project-2/blob/main/Ind%20Sam%20Work/Data_Viz_Sam.ipynb). All required charting saved in [Charts](https://github.com/Corzalite/Group-17-project-2/tree/main/Charts) folder. 

## Question 3

How does the length of a campaign compare to the success/failure of our selected countries?

Visualization of the data does not show a solid correlation between the length of the campaign and its success or failure. 

[chart_all.png](https://github.com/Corzalite/Group-17-project-2/blob/main/Charts/chart_all.png)

When looked by individual countries the US has successful campaigns across most days, but the least successful in the shortest and the longest days. Canada has the most success between approximately 225 and 250 days, China between 275 and 300, and Australia around 50 days. All countries had success with shorter and longer campaigns. 

The length of the campaign is only one factor, other factors should be explored such as the type of play, the time of year in the specific country, the goal, etc.

Individual query and charting work done in [IND_Marty_work/ETL_Data_Viz](https://github.com/Corzalite/Group-17-project-2/tree/main/IND_Marty_work). All required charting saved in [Charts](https://github.com/Corzalite/Group-17-project-2/tree/main/Charts) folder.
