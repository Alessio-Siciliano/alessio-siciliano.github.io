---
title: Bigquery
weight: 1
prev: /bigquery-advanced-utils/modules
---

## Introduction

The `BigQueryClient` class is a custom extension of the Google Cloud BigQuery Client. This enhanced client provides additional functionality for managing BigQuery operations more efficiently. It includes built-in methods for managing permissions, handling datasets and tables, and automating common tasks such as loading data, exporting tables, and simulating queries.

## Class Initialization
This constructor initializes the `BigQueryClient` class, which inherits from the `google.cloud.bigquery.Client`. It shares the attributes and behavior of the original BigQuery client while enabling customized extensions for easier BigQuery operations.
#### Parameters
* `project_id` (str): The project ID associated with the BigQuery client.
* `credentials` (Optional[Credentials]): The credentials used to authenticate the client.
* `_http` (Optional[requests.Session]): The HTTP session to use for requests.
* `location` (Optional[str]): Default geographic location for queries and jobs.
* `default_query_job_config` (Optional[QueryJobConfig]): Default configuration for query jobs.
* `default_load_job_config` (Optional[LoadJobConfig]): Default configuration for load jobs.
* `client_info` (Optional[ClientInfo]): Information about the client.
* `client_options` (Optional[Union[ClientOptions, Dict]]): Additional client options.
#### Example
```python
BigQueryClient(
    project_id: str,
    credentials: Optional[Credentials] = None,
    _http: Optional[requests.Session] = None,
    location: Optional[str] = None,
    default_query_job_config: Optional[QueryJobConfig] = None,
    default_load_job_config: Optional[LoadJobConfig] = None,
    client_info: Optional[ClientInfo] = None,
    client_options: Optional[Union[ClientOptions, Dict]] = None,
)
```

## Methods Overview

### `check_table_existence`
#### Description
Checks whether a specific table exists within a given dataset.
#### Parameters
* `dataset_id` (str): The ID of the dataset to check.
* `table_id` (str): The ID of the table to check.
#### Example
```python
exists = client.check_table_existence("my_dataset", "my_table")
print(f"Table exists: {exists}")
```

### `load_data_from_csv`
#### Description
Loads data from a CSV file into a specified BigQuery table. Optionally applies validation tests (custom or not) to the data.
#### Parameters
* `dataset_id` (str): The destination dataset ID.
* `table_id` (str): The destination table ID.
* `csv_file_path` (str): Path to the CSV file.
* `test_functions` (Optional[list]): A list of validation functions applied to the data. For the full list of predefined test (See the [Custom checks class](/bigquery-advanced-utils/modules/custom_data_checks) page for more details.)
* `encoding` (str): The file encoding (default is UTF-8).

#### Example
```python
from functools import partial

def custom_test(index, row, header, column_sums):
    if len(row) != len(header):
        raise ValueError(f"Row {index} does not match header length.")

data_checks = CustomDataChecks()
client.load_data_from_csv(
    dataset_id="my_dataset",
    table_id="my_table",
    csv_file_path="data.csv",
    test_functions=[
      custom_test,
      partial(data_checks.check_columns),
      partial(
        data_checks.check_unique, columns_to_test=["col1"],
      ),
      ...
    ]
)
```



### `simulate_query`
#### Description
Simulates a query execution to estimate resource usage and provides metadata such as schema and referenced tables.
#### Parameters
* `query` (str): The SQL query to simulate.
#### Returns
* `dict`: Metadata about the query execution, including schema, referenced tables, and bytes processed.
#### Example
```python
simulation = client.simulate_query("SELECT * FROM `my_project.my_dataset.my_table` LIMIT 10")
print(simulation)
```

### `grant_permission`
#### Description
Manages permissions (add, remove, or update) for users on a BigQuery table or dataset.
#### Parameters
* `resource_id` (str): The resource ID in the format project_id.dataset_id (if dataset) or project_id.dataset_id.table_id (if table).
* `user_permissions` (List[Dict[str, str]]): A list of dictionaries containing user_email and role.
* `action` (str): The action to perform (add, remove, or update).
#### Example
```python
permissions = [
    {"user_email": "user@example.com", "role": "READER"},
    {"user_email": "admin@example.com", "role": "OWNER"}
]

client.grant_permission(
    resource_id="my_project.my_dataset",
    user_permissions=permissions,
    action="add"
)
```

### `export_table`
#### Description
Exports a BigQuery table to a specified format (e.g., CSV, JSON) to Cloud Storage.
#### Parameters
* `dataset_id` (str): The ID of the dataset.
* `table_id` (str): The ID of the table.
* `destination` (str): The destination path (e.g., `gs://bucket_name/file`).
* `output_file_format` (OutputFileFormat): The format of the exported file (`CSV`, `JSON`, or `AVRO`).
* `compression` (Literal): Compression type (`GZIP`, `DEFLATE`, `SNAPPY`, or `NONE`).
#### Example
```python
client.export_table(
    dataset_id="my_dataset",
    table_id="my_table",
    destination="gs://my_bucket/my_table.csv",
    output_file_format="CSV",
    compression="GZIP"
)
```