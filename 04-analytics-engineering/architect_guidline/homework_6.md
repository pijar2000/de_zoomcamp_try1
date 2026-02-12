### Question 6. Build a Staging Model for FHV Data

by pijar

Create a staging model for the **For-Hire Vehicle (FHV)** trip data for 2019.

1. Load the [FHV trip data for 2019](https://github.com/DataTalksClub/nyc-tlc-data/releases/tag/fhv) into your data warehouse
2. Create a staging model `stg_fhv_tripdata` with these requirements:
   - Filter out records where `dispatching_base_num IS NULL`
   - Rename fields to match your project's naming conventions (e.g., `PUlocationID` → `pickup_location_id`)

What is the count of records in `stg_fhv_tripdata`?

- First you need to download and upload the dataset to gcs bucket, then make external table for it (modules 3 step by step)
  
<img width="783" height="658" alt="image" src="https://github.com/user-attachments/assets/f5afd87b-f61b-472b-8b9c-feacf393714a" />

then, you need to modify you `sources.yml` in models -> staging folder, scroll all the way down, and add this line

```yml
- name: fhv_tripdata #this is variable that will be called by stg_fhv_tripdata.sql
        description: anything lah
          Raw FHV (For-Hire Vehicle) trip records for 2019.
          Data is loaded from GCS parquet files.
        identifier: fhv_tripdata #this is your table name
```

- after that still in staging folder you will add .sql file with this pattern

```sql
{{ config(materialized='view') }}

with tripdata as 
(
  select *
  from {{ source('raw','fhv_tripdata') }} --this will be point out your souces.yml file, calling out fhv_tripdata variable
  where dispatching_base_num is not null --parameter to filter out
)
select
    dispatching_base_num,
    cast(pickup_datetime as timestamp) as pickup_datetime,
    cast(dropoff_datetime as timestamp) as dropoff_datetime,
    cast(pulocationid as integer) as pickup_location_id,
    cast(dolocationid as integer) as dropoff_location_id,
    sr_flag,
    affiliated_base_number
from tripdata
```

After that you can run in your dbt folder

```bash
dbt run --select stg_fhv_tripdata
```

- remember you run it without --prod it means you will send the materialized view table to your dev environment

<img width="394" height="442" alt="image" src="https://github.com/user-attachments/assets/13ee8fa8-8eec-4657-b463-7bfe9ea4e0e4" />

Here you can proceed your table to count the value
