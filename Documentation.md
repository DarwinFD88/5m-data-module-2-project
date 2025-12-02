# Step-by-Step Guide

1. Add the Extractor (Tap) 
For local files, you can use a generic file-based tap or create a custom one. A common approach is to use tap-csv for CSV files.

```bash
meltano add extractor tap-csv
```

2. Configure the Extractor
Set the path to your local data directory and specify the data format. This is done in your meltano.yml file or using the CLI. 

```bash
# Set the root directory for the extractor
meltano config tap-csv set root_dir /path/to/your/local/data/directory

# Configure stream maps (optional, but often necessary to define table names)
meltano config tap-csv set stream_maps '{"*": {"table_name": "your_bigquery_table"}}'

# Define schema handling if necessary
```

3. Add the Loader 
Add the target-bigquery loader to your project. 

```bash
meltano add loader target-bigquery
```

4. Configure the Loader 
Set up the connection details for BigQuery, primarily using the service account key file. 
Set the project_id, dataset_id, and credentials_path.
The dataset_id can default to the tap's namespace if left unset. 

```bash
# Set the Google Cloud project ID
meltano config target-bigquery set project_id <YOUR_PROJECT_ID>

# Set the path to your service account key file
meltano config target-bigquery set credentials_path /path/to/your/client_secrets.json

# (Optional) Set the dataset ID
meltano config target-bigquery set dataset_id <YOUR_DATASET_ID>
```

5. Run the EL (Extract & Load) Pipeline 
Execute the pipeline using the meltano elt command to extract data from the local directory and load it into BigQuery. 

```bash
meltano elt tap-csv target-bigquery --job_id=local_files_to_bigquery
```