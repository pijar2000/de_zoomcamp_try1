## Question 2

What is the rendered value of the variable file when the inputs taxi is set to `green`, year is set to `2020`, and month is set to `04` during execution?

- We should remember that in flow code `04_postgres_taxi.yaml` there is line

```yaml
variables:
  file: "{{inputs.taxi}}_tripdata_{{inputs.year}}-{{inputs.month}}.csv" # this one
  staging_table: "public.{{inputs.taxi}}_tripdata_staging"
  table: "public.{{inputs.taxi}}_tripdata"
  data: "{{outputs.extract.outputFiles[inputs.taxi ~ '_tripdata_' ~ inputs.year ~ '-' ~ inputs.month ~ '.csv']}}"
```
- the keys is that will be three variable, taxi type, year, and month
