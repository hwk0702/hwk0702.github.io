---

layout: post

title: "SQL Data Types"

date: 2020-01-13 14:50:07

categories: [Data Engineering/SQL]

description:

image: /img/sql.png

published: true

canonical_url:

---

## SQL Data Types

<br> <img src="/img/sqldata.png">

### SQL Numeric Data Types

|DATATYPE|FROM|TO|
|:--------:|:----:|:--:|
|bit|0|1|
|tinyint|0|255|
|smallint|-32,768|-32,767|
|int|-2,147,483,648|2,147,483,647|
|bigint|-9,223,372,036,854,775,808|9,223,372,036,854,775,807|
|decimal|-10^38 + 1|10^38 - 1|
|numeric|-10^38 + 1|10^38 - 1|
|float|-1.79E + 308|1.79E + 308|
|real|-3.40E +38|3.40E +38|

### SQL Date and Time Data Type

|DATATYPE|DESCRIPTION|
|:------:|:----------|
|DATE|Stores data in the format YYYY-MM-DD|
|TIME|Stores time in the format HH:MI:SS|
|DATETIME|Stores date and time information in the format YYYY-MM-DD HH:MI:SS|
|TIMESTAMP|Stores number of seconds passed since the Unix epoch('1970-01-01 00:00:00' UTC)|
|YEAR|Stores year in 2 digit or 4 digit format. Range 1901 to 2155 in 4-digit format. Range 70 to 69, representing 1970 to 2069|

### SQL Character and String Data Types

|DATATYPE|DESCRIPTION|
|:------:|:----------|
|CHAR|Fixed length with maximum length of 8,000 Characters|
|VARCHAR|Variable length storage with maximum length 8,000 Characters|
|VARCHAR(max)|Variable length storage with provided max characters, not suppoerted in MYSQL|
|TEXT|Variable length storage with maximum size of 2GB data|
