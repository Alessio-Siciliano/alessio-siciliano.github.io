---
title: Datatransfer
weight: 2
prev: /bigquery-utils/modules/bigquery
next: /bigquery-utils/modules/bigquery
toc_depth: 2
sidebar:
  open: true
cascade:
  type: docs
---

## Introduction

This module provides a custom implementation of the `DataTransferServiceClient` to extend its functionality. It allows advanced querying of scheduled transfers in BigQuery, adding features like caching and filtering by owner email or table.

## Class Initialization
The `DataTransferClient` extends the original Google Cloud `DataTransferServiceClient` to provide additional utility methods for managing scheduled queries in BigQuery. The enhancements include caching, advanced filtering, and integration with string utilities.
#### Parameters
* `credentials` (str): The user’s credentials for authentication.
* `client_options` (Optional): A dictionary of custom client settings.

#### Example
```python
DataTransferClient(
    credentials: Optional[Credentials] = None,
    client_options: Optional[Union[ClientOptions, Dict]] = None,
    def __init__(self, credentials: Optional[Credentials] = None, client_options: Optional[dict] = None) -> None

)
```

## Methods Overview

### `list_transfer_configs`
#### Description
Retrieves all scheduled queries in a project. Optionally, fetches the email of the owner for each transfer configuration.
#### Parameters
* `dataset_id` (str): The ID of the dataset to check.
* `table_id` (str): The ID of the table to check.
* `request` Optional: A ListTransferConfigsRequest object or equivalent dictionary.
* `parent` Optional: The project and location in the format `projects/{project_id}/locations/{location_id}`.
* `retry` Optional: Retry configuration for handling errors.
* `timeout` Optional: Timeout for the request.
* `metadata` Optional: Additional metadata for the request.
* `with_email` Optional: Whether to fetch the email of the transfer config owner (default is False).

#### Example
```python
configs = client.list_transfer_configs(parent="projects/my-project/locations/my-location")
```

### `list_transfer_config_by_owner_email`
#### Description
Filters transfer configurations by the email of the owner.
#### Parameters
* `owner_email`: The email of the owner to filter by.
* `parent`: The project and location in the format `projects/{project_id}/locations/{location_id}`.

#### Example
```python
configs = client.list_transfer_config_by_owner_email(
    owner_email="user@example.com", 
    parent="projects/my-project/locations/us"
)
```


### `list_transfer_configs_by_table`
#### Description
Filters transfer configurations by the table referenced in their queries.
#### Parameters
* `table_id` (str): The name of the table to filter by (not the full path).
#### Returns
* `parent`: The project and location in the format `projects/{project_id}/locations/{location_id}`.
#### Example
```python
configs = client.list_transfer_configs_by_table(
  table_id="my_table",
  parent="projects/my-project/locations/us"
)
```
