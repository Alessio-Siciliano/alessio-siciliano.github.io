---
title: Constants
weight: 1
prev: /bigquery-utils/modules/utils
next: /bigquery-utils/modules/utils
cascade:
  type: docs
---

## Overview
This module defines the constants used throughout the project. It includes general-purpose constants, logging message templates, and configuration values for integration with Google BigQuery. The constants are designed to ensure consistency and reduce hardcoding across the codebase.


## Constants

### **General Constants**
- **`DEFAULT_LOG_LEVEL`**: `"DEBUG"`  
  Default log level for the application, used to control the verbosity of logs.


### **Logging Messages**
These constants define standard logging messages used throughout the project:
- **`LOG_SUCCESS`**: `"SUCCESS"`  
  Message indicating successful operations.
- **`LOG_FAILED`**: `"FAILED"`  
  Message indicating failed operations.
- **`LOG_UNHANDLED_EXCEPTION`**: `"UNHANDLED EXCEPTION"`  
  Message used for unhandled exceptions in the application.


### **BigQuery-Specific Constants**
These constants relate to Google BigQuery configurations:

- **`IAM_TO_DATASET_ROLES`**: A dictionary mapping IAM roles to BigQuery dataset roles:
```python 
{
    "roles/bigquery.dataViewer": "READER",
    "roles/bigquery.dataEditor": "WRITER",
    "roles/bigquery.dataOwner": "OWNER",
}
```
Used for role-based access control (RBAC) in BigQuery datasets.

- **`OUTPUT_FILE_FORMAT`**: A dictionary mapping file format names to `SourceFormat` constants in BigQuery:
```python
{
    "CSV": SourceFormat.CSV,
    "JSON": SourceFormat.NEWLINE_DELIMITED_JSON,
    "AVRO": SourceFormat.AVRO,
}
```
Specifies the formats for output files in BigQuery export operations.


### **Type Literals**
These type literals define specific sets of values to ensure type safety in various operations:

- **`PartitionTimeGranularities`**: Allowed values for partition time granularity in BigQuery tables:
```python
Literal["HOUR", "DAY", "MONTH", "YEAR"]
```

- **`OutputFileFormat`**: Allowed output file formats for BigQuery export operations:
```python
Literal["CSV", "JSON", "AVRO"]
```

- **`PermissionActionTypes`**: Allowed action types for permission management:
```python
Literal["ADD", "REMOVE", "UPDATE"]
```

## Example Usage

### **Using Logging Messages**
```python
import logging
from constants import LOG_SUCCESS, LOG_FAILED

def log_operation_success():
    logging.info("Job %s loaded!",LOG_SUCCESS)

def log_operation_failure():
    logging.error("Problem iwth the job [%s]", LOG_FAILED)
```

### **Mapping IAM Roles**
```python 
from constants import IAM_TO_DATASET_ROLES

def get_dataset_role(iam_role):
    return IAM_TO_DATASET_ROLES.get(iam_role, "UNKNOWN")
```

### **Setting Output Formats**
```python
from constants import OUTPUT_FILE_FORMAT

def export_data(file_format):
    if file_format in OUTPUT_FILE_FORMAT:
        return OUTPUT_FILE_FORMAT[file_format]
    else:
        raise ValueError("Invalid file format")
```

## Dependencies
- **`google-cloud-bigquery`**: Provides the `SourceFormat` class for file formats in BigQuery.


## Notes
This module is designed to centralize project constants to improve maintainability and reduce the risk of errors due to hardcoded values.
