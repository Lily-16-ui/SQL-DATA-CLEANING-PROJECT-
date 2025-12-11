# SQL DATA CLEANING PROJECT(SALES DATASET)

## TABLE OF CONTENTS
- [Project Overview](#project-overview)
- [Objectives](#objectives)
- [Data Source](#data-source)
- [Step by step Cleaning Process](#step-by-step-cleaning-process)
- [Key SQL concepts used](#key-sql-concepts-used)
- [Final results](#final-results)

### PROJECT OVERVIEW

This project contains my first full data-cleaning workflow in SQL.
I used SQL Server to clean, transform, and standardize a sales dataset downloaded from Kaggle.

### OBJECTIVES

* Clean date fields
* Standardize text values
* Create new cleaned columns
* Format numeric fields
* Rename columns for clarity
* Drop outdated or redundant columns

### DATA SOURCE

Sales dataset from Kaggle
Imported as: dbo.Book1

### STEP BY STEP CLEANING PROCESS 

SELECT *
FROM [dbo].[Book1]

TO SELECT EVERYTHING FROM THE IMPORTED TABLE

SELECT ORDERDATE, REPLACE(ORDERDATE, '00:00:00.0000000', '') AS DATEORDERED
FROM [dbo].[Book1] 

REMOVING THE TIIME AND RETAINING ONLY THE DATE FROM THE ORDERDATE COLUMN RENAMING IT AS DATEORDERED

ALTER TABLE [dbo].[Book1]
ADD DATEORDERED DATE
  
ADDING THE NEWLY CREATED COLUMN ‘DATEORDERED’ TO THE TABLE 

UPDATE [dbo].[Book1]
SET DATEORDERED = CAST(ORDERDATE AS DATE) 

IMPORTING THE VALUES INTO THE COLUMN

ALTER TABLE [dbo].[Book1]
DROP COLUMN ORDERDATE 

DELETING THE ORDERDATE COLUMN

SELECT 
ROUND(PRICEEACH, 1) AS PRODUCTPRICE,  
ROUND(SALES, 1) AS SALE 
FROM [dbo].[Book1]  

ROUNDING UP THE VALUES IN ‘PRICEEACH’ AND ‘SALES’ COLUMN TO ONE DECIMAL PLACE, AND RENAMING THEM AS ‘PRODUCTPRCE’ AND ‘SALE’.

ALTER TABLE [dbo].[Book1] 
ADD PRODUCTPRICE DECIMAL(10, 1)

ADDING THE PRODUCTPRICE COLUMN TO THE TABLE

ALTER TABLE [dbo].[Book1] 
ADD SALE DECIMAL(10, 1)

ADDING THE SALE COLUMN TO THE TABLE

UPDATE [dbo].[Book1]
SET PRODUCTPRICE = ROUND(PRICEEACH, 1),
SALE = ROUND(SALES, 1) 

ADDING VALUES TO BOTH COLUMNS

ALTER TABLE [dbo].[Book1]
DROP COLUMN PRICEEACH

DELETING THE PRICEEACH COLUMN

ALTER TABLE [dbo].[Book1]
DROP COLUMN SALES

DELETING THE SALES COLUMN

UPDATE [dbo].[Book1]
SET TERRITORY = CASE TERRITORY
WHEN 'NA' THEN 'North America'
WHEN 'APAC' THEN 'Asia Pacific'
WHEN 'EMEA' THEN 'Europe, Middle East, Africa' 
ELSE TERRITORY 
END 

RENAMING CERTAIN ENTIES UNDER THE TERRITORY COLUMN

UPDATE [dbo].[Book1]
SET COUNTRY = CASE COUNTRY
WHEN 'USA' THEN 'United States Of America'
WHEN 'UK' THEN 'United Kingdom'
ELSE COUNTRY 
END 

RENAMING ENTRIES UNDER THE COUNTRY COLUMN

EXEC sp_rename '[dbo].[Book1].QUATERLY_ID', 'QUATER', 'COLUMN' 

EXEC sp_rename '[dbo].[Book1].MSRP', 'MANUFACTURER SUGGESTED RETAIL PRICE', 'COLUMN' 

EXEC sp_rename '[dbo].[Book1].MONTH_ID', 'MONTH', 'COLUMN' 

EXEC sp_rename '[dbo].[Book1].YEAR_ID', 'YEAR', 'COLUMN' 

EXEC sp_rename '[dbo].[Book1].ADDRESSLINE1', 'ADDRESS', 'COLUMN'
RENAMING COLUMN HEADERS 

### FINAL RESULTS 

- Cleaned date fields
- Standardized territory and country names
- Improved numerical consistency (rounded to 1 decimal)
- Improved schema readability
- Removed redundant fields

### KEY SQL CONCEPTS USED

* ALTER TABLE
* UPDATE
* CAST
* ROUND
* CASE WHEN
* sp_rename
* SELECT 
