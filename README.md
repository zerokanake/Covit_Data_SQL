# COVID-19 Data Analysis with SQL

This project focuses on analyzing COVID-19 data using SQL to uncover patterns, trends, and insights from the pandemic. The analysis includes key metrics such as case trends, vaccination rates, mortality rates, and highly infection rate across various regions. 



## Project Description

The project involves:

- **Data Cleaning**: Ensuring the dataset is accurate, consistent, and ready for analysis.
- **Exploratory Data Analysis (EDA)**: Using SQL to explore data trends and patterns.
- **Key Insights**: Identifying metrics such as:
  - Trends in daily cases and deaths.
  - Vaccination progress by region.
  - Recovery rates and their correlation with healthcare infrastructure.
  - Geographical comparisons of COVID-19 impact.

## Key Skills Demonstrated

- **SQL Querying**: Expertise in writing efficient SQL queries to manipulate and analyze data.
- **Data Cleaning**: Handling missing or inconsistent data to ensure accurate results.
- **Data Aggregation**: Summarizing large datasets to extract key insights.


## Tools and Technologies

- **SQL**: For data querying, cleaning, and analysis.
- **Database Management System**: PostgreSQL Server.

## Dataset

The dataset used in this project is sourced from [Kaggle](https://www.kaggle.com/datasets/sanaaafrine/covid-19-dataset).

## Data Query
- **Death Percentage by Location**: 
This query calculates the death percentage based on total cases and total deaths for locations containing "Jap" in their name, while excluding null continents. It demonstrates skills in filtering, data transformation, and calculating derived metrics.

``` sql
SELECT location, date, total_cases,  total_deaths, cast(total_deaths as decimal) / total_cases*100 as death_percentage
FROM CovidDeaths
where LOCATION LIKE '%Jap%'
and continent is not null
```
- **Calculate the Percentage of Population Infected by COVID-19**: This query calculates the percentage of the population infected for specific locations.

```sql
select date, location, population, total_cases, cast(total_cases as decimal)/population*100  as percentagePopulationInfected
FROM CovidDeaths
WHERE continent is not null
where location like '%Jap%' and continent is not null
```
- **Population vs. Vaccination Trends**: This query calculates cumulative vaccination numbers by location.

``` sql
SELECT dea.continent, dea.location, to_date(dea.date, 'MM/DD/YYYY'), dea.population, vac.new_vaccinations,
SUM(vac.new_vaccinations) over (PARTITION BY dea.location ORDER BY dea.location, dea.date) 
as Rolling_people_Vaccinated,
FROM CovidDeaths as dea
JOIN covidvaccination as vac
ON dea.location = vac.location and dea.date = vac.date
WHERE dea.continent is not null
ORDER BY 2, 3
```
