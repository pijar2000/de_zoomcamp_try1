# Homework 3 Guideline

By Pijar HM

- Make your own google project

<img width="1222" height="712" alt="image" src="https://github.com/user-attachments/assets/5bf73e42-eabe-424e-9373-c45850b05cef" />

Then, I use google cli to get credentials

- First you should login to google cli with your terminal, in my case i used powershell

```powershell
gcloud auth login
```

- After that, you will need to test where is your credential file, for me it is in `C:\Users\pijar2000\AppData\Local\Google\Cloud SDK\google-cloud-sdk\bin\gcloud.cmd`

- In python ingesting script `load_yellow_taxi_data.py` , i made some modification for credential login

```python
# If commented initialize client with the following

client = storage.Client(project='zoomcamp-mod3-datawarehouse') # I change this

```

i changed it to

```python
def get_credentials():
    gcloud_path = r"C:\Users\pijar2000\AppData\Local\Google\Cloud SDK\google-cloud-sdk\bin\gcloud.cmd"

    result = subprocess.run(
        [gcloud_path, 'auth', 'print-access-token'],
        capture_output=True,
        text=True,
        check=True
    )
    token = result.stdout.strip()
    from google.oauth2.credentials import Credentials
    return Credentials(token=token)

credentials = get_credentials()
client = storage.Client(credentials=credentials, project='project-475f5f46-e321-4ab4-93e')
```

- `project-475f5f46-e321-4ab4-93e` is my project id you should change it to your project id
- Don't forget to change your bucket name too, for me its `dezoomcamp_hw3_2026_pijar`

- After that you can run the script `load_yellow_taxi_data.py`

<img width="1494" height="963" alt="image" src="https://github.com/user-attachments/assets/6514bafd-119c-471c-a4ad-ab6a99ab33cd" />

Check your bucket in google cloud, then you will find something like that

- After that, make your own external table, if there's no schema, make one
- Careful change the rest with your own bucket name and you own project name

```sql
CREATE SCHEMA IF NOT EXISTS
`zoomcamp-pijar.nytaxi`
OPTIONS (location = 'US');


CREATE OR REPLACE EXTERNAL TABLE
`zoomcamp-pijar.nytaxi.external_yellow_tripdata_2024`
OPTIONS (
  format = 'PARQUET',
  uris = ['gs://dezoomcamp_hw3_2026_pijar/yellow_tripdata_2024-*.parquet']
);
```

- After that make your materialiazed table

```sql
CREATE OR REPLACE TABLE
`zoomcamp-pijar.nytaxi.yellow_tripdata_2024`
AS
SELECT *
FROM `zoomcamp-pijar.nytaxi.external_yellow_tripdata_2024`;
```

You should see something like this

<img width="439" height="545" alt="image" src="https://github.com/user-attachments/assets/a2f86502-31fa-4704-b05d-190850d4c080" />
