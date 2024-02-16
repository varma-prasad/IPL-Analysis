# IPL-Analysis

## Table of Contents

* [Overview](#overview)
* [Create Tables](#create-table-queries)
* [Problem Statement 1](#analysis1)
* [Problem Statement 2](#analysis2)
* [Problem Statement 3](#analysis3)
* [Problem Statement 4](#analysis4)
* [Problem Statement 5](#analysis5)



### Overview

  1. Perform Sports anlytics of famous cricketing festival of india "Indian Premier League" from 2008 to 2020
  2. WE have two data sets having Ball-by-Bal data and Match-Wise Data
  3. Create necessary table structure in PG Admin and import CSV data and perform analytics for different scenarios.
  4. Present queries to fetch data and results of the analysed data

### Create Table Queries

Create a table named ‘deliveries’ with appropriate data types for columns
```
-- Table: public.deliveries
-- DROP TABLE IF EXISTS public.deliveries;
CREATE TABLE IF NOT EXISTS public.deliveries
(
    id integer NOT NULL,
    inning integer NOT NULL,
    over integer,
    ball integer,
    batsman character varying COLLATE pg_catalog."default",
    non_striker character varying COLLATE pg_catalog."default",
    bowler character varying COLLATE pg_catalog."default",
    batsman_runs integer,
    extra_runs integer,
    total_runs integer,
    is_wicket integer,
    dismissal_kind character varying COLLATE pg_catalog."default",
    player_dismissed character varying COLLATE pg_catalog."default",
    fielder character varying COLLATE pg_catalog."default",
    extras_type character varying COLLATE pg_catalog."default",
    batting_team character varying COLLATE pg_catalog."default",
    bowling_team character varying COLLATE pg_catalog."default",
    CONSTRAINT "FK_MATCH_ID" FOREIGN KEY (id)
        REFERENCES public.matches ("ID") MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
        NOT VALID
)

TABLESPACE pg_default;

ALTER TABLE IF EXISTS public.deliveries
    OWNER to postgres;

Create a table named ‘matches’ with appropriate data types for columns

-- Table: public.matches
-- DROP TABLE IF EXISTS public.matches;
CREATE TABLE IF NOT EXISTS public.matches
(
    id integer NOT NULL,
    city character varying COLLATE pg_catalog."default",
    date date,
    player_of_match character varying COLLATE pg_catalog."default",
    venue character varying COLLATE pg_catalog."default",
    neutral_venue integer,
    team1 character varying COLLATE pg_catalog."default",
    team2 character varying COLLATE pg_catalog."default",
    toss_winner character varying COLLATE pg_catalog."default",
    toss_decision character varying COLLATE pg_catalog."default",
    winner character varying COLLATE pg_catalog."default",
    result character varying COLLATE pg_catalog."default",
    result_margin integer,
    eliminator "char",
    method character varying COLLATE pg_catalog."default",
    umpire1 character varying COLLATE pg_catalog."default",
    umpire2 character varying COLLATE pg_catalog."default",
    CONSTRAINT "IPL_MATCH_pkey" PRIMARY KEY (id)
)

TABLESPACE pg_default;

ALTER TABLE IF EXISTS public.matches
    OWNER to postgres;
```

### Analysis1

Write a query to fetch the year-wise total runs scored at Eden Gardens and order it in the descending order of total runs scored
```
select 
	to_char(date,'yyyy'),sum(total_runs)
from 
	deliveries d inner join matches m
	on  m.id = d.id
where 
	venue = 'Eden Gardens'
group by 
	to_char(date,'yyyy');
```
Output:\
![image](https://github.com/varma-prasad/IPL-Analysis/assets/108605375/1a3c942e-15ed-4164-bc49-2dc2cbe11546)

### Analysis2

Fetch data of all the matches where the result mode is ‘runs’ and margin of victory is more than 100 runs.
```
select 
	* 
from 
	matches
where 
	result = 'runs' and result_margin > 100;
```
Output:\
![image](https://github.com/varma-prasad/IPL-Analysis/assets/108605375/02d627f6-4605-4533-a16c-abbbca9f3f02)

### Analysis3

Write a query to fetch the total number of boundaries scored by each team 
```
select 
	batting_Team,ball_result,count(*) as Boundaries
from 
	deliveries_v02
where
	ball_result in ('Four','Six')
group by
	batting_Team,ball_result
order by 
	Ball_result Desc, Boundaries desc;
```
Output:\
![image](https://github.com/varma-prasad/IPL-Analysis/assets/108605375/fb269103-f0bc-4663-946d-fcf30d2dca1c)

### Analysis4

Write a query to get the top 5 bowlers who conceded maximum extra runs 

```
select 
	Bowler, sum(Extra_Runs) as Total_Extras
from
	deliveries
group by 
	Bowler
order by 
	Total_Extras desc
limit 5;
```
Output:\
![image](https://github.com/varma-prasad/IPL-Analysis/assets/108605375/edf55f56-27bd-414e-ab38-c853aca86926)

### Analysis5

Write a query to fetch the total number of boundaries and dot balls 
```
select 
	ball_result,count(*)
from 
	deliveries_v02
where
	ball_result in ('Dot','Four','Six')
group by
	ball_result;
```
Output:\
![image](https://github.com/varma-prasad/IPL-Analysis/assets/108605375/c8baba8b-3ce4-4dae-b3fa-abef4f1c316f)

## 🛠 Tools used
![](https://img.shields.io/badge/postgresql-v16.2-blue)


## Authors

- [Varma Prasad S](https://github.com/varma-prasad)

## 🛠 Skills
SQL, ETL, Python, Power BI...

## 🔗 Links

[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/varma-prasad-s/)

   
