# DATA CLEANING
## Project Description
This is an educational project on data cleaning and preparation using SQL. The original database in CSV format is located in the file club_member_info.csv. Here, we will explore the steps that need to be applied to obtain a cleansed version of the dataset.

### Get the 10 first rows from the table using SQL console
```sql
SELECT *
FROM club_member_info
LIMIT 10;
```
|full_name|age|martial_status|email|phone|full_address|job_title|membership_date|
|---------|---|--------------|-----|-----|------------|---------|---------------|
|addie lush|40|married|alush0@shutterfly.com|254-389-8708|3226 Eastlawn Pass,Temple,Texas|Assistant Professor|7/31/2013|
|      ROCK CRADICK|46|married|rcradick1@newsvine.com|910-566-2007|4 Harbort Avenue,Fayetteville,North Carolina|Programmer III|5/27/2018|
|Sydel Sharvell|46|divorced|ssharvell2@amazon.co.jp|702-187-8715|4 School Place,Las Vegas,Nevada|Budget/Accounting Analyst I|10/6/2017|
|Constantin de la cruz|35||co3@bloglines.com|402-688-7162|6 Monument Crossing,Omaha,Nebraska|Desktop Support Technician|10/20/2015|
|  Gaylor Redhole|38|married|gredhole4@japanpost.jp|917-394-6001|88 Cherokee Pass,New York City,New York|Legal Assistant|5/29/2019|
|Wanda del mar       |44|single|wkunzel5@slideshare.net|937-467-6942|10864 Buhler Plaza,Hamilton,Ohio|Human Resources Assistant IV|3/24/2015|
|Joann Kenealy|41|married|jkenealy6@bloomberg.com|513-726-9885|733 Hagan Parkway,Cincinnati,Ohio|Accountant IV|4/17/2013|
|   Joete Cudiff|51|divorced|jcudiff7@ycombinator.com|616-617-0965|975 Dwight Plaza,Grand Rapids,Michigan|Research Nurse|11/16/2014|
|mendie alexandrescu|46|single|malexandrescu8@state.gov|504-918-4753|34 Delladonna Terrace,New Orleans,Louisiana|Systems Administrator III|3/12/1921|
| fey kloss|52|married|fkloss9@godaddy.com|808-177-0318|8976 Jackson Park,Honolulu,Hawaii|Chemical Engineer|11/5/2014|

### Make a copy of your table
#### Create a new table for cleaning
Let's generate a new table where we can manipulate and restructure the data without modifying the original dataset.
```sql
CREATE TABLE "club_member_info_clean" (
	full_name VARCHAR(50),
	age INTEGER,
	martial_status VARCHAR(50),
	email VARCHAR(50),
	phone VARCHAR(50),
	full_address VARCHAR(50),
	job_title VARCHAR(50),
	membership_date VARCHAR(50)
);
```
#### Copy all values from original table
```sql
INSERT INTO club_member_info_clean
SELECT * FROM club_member_info;
```
### Clean data and document it
#### For example
1. Inconsistent letter case
2. Age out of realistic range
3. Leading and trailing whitespaces
4. Email is null

```sql
SELECT 
  UPPER(TRIM(full_name)) AS full_name_cleaned,
  CASE 
    WHEN age < 0 OR age > 100 THEN NULL 
    ELSE age 
  END AS age_cleaned,
  TRIM(email) AS email_cleaned
FROM club_member_info_clean
LIMIT 10;
```
|full_name_cleaned|age_cleaned|email_cleaned|
|-----------------|-----------|-------------|
|ADDIE LUSH|40|alush0@shutterfly.com|
|ROCK CRADICK|46|rcradick1@newsvine.com|
|SYDEL SHARVELL|46|ssharvell2@amazon.co.jp|
|CONSTANTIN DE LA CRUZ|35|co3@bloglines.com|
|GAYLOR REDHOLE|38|gredhole4@japanpost.jp|
|WANDA DEL MAR|44|wkunzel5@slideshare.net|
|JOANN KENEALY|41|jkenealy6@bloomberg.com|
|JOETE CUDIFF|51|jcudiff7@ycombinator.com|
|MENDIE ALEXANDRESCU|46|malexandrescu8@state.gov|
|FEY KLOSS|52|fkloss9@godaddy.com|
