---
title: Custom Data Checks Module Documentation
linkTitle: Custom Data Checks
weight: 2
prev: /bigquery-utils/modules/utils/constants
next: /bigquery-utils/modules/utils/numeric
cascade:
  type: docs
---

## Introduction
This module provides a comprehensive set of functions to validate and check the integrity of data in tabular formats such as CSVs. These checks help ensure the correctness of data by validating rows, columns, and specific values against given criteria.
### Key Features
- **Column Validation:** Ensures uniform row lengths and column existence.
- **Uniqueness Check:** Detects duplicate values in specified columns.
- **Null Checks:** Validates that specified columns do not contain null values.
- **Numeric Range Validation:** Confirms numeric values fall within a specified range.
- **String Pattern Matching:** Verifies strings match a specified regex pattern.
- **Date Format Validation:** Ensures dates adhere to a given format.
- **Datatype Validation:** Confirms values match the expected datatype.
- **Value Set Check:** Ensures values exist within a specified set.

## Class Initialization

To use the `CustomDataChecks` utilities, you first need to create an instance of the class:

```python
from bigquery_advanced_utils.utils.custom_data_checks import CustomDataChecks

custom_data_checks_util = CustomDataChecks()
```

The `CustomDataChecks` class does not require any parameters during initialization. Once instantiated, you can call its methods for various string manipulation tasks.

## Methods Overview
### `check_columns`

Validates that all rows in a dataset have the same number of columns as the header.

#### Parameters
- `idx (int)`: Row number.
- `row (list)`: List of values in the row.
- `header (list)`: List of column names.
- `column_sums (list)`: (Unused) Placeholder for memory storage.

#### Raises
- `ValueError`: If row lengths do not match the header length.

### `check_unique`
Ensures specified columns contain unique values across all rows.

#### Parameters
- `idx (int)`: Row number.
- `row (list)`: List of values in the row.
- `header (list)`: List of column names.
- `column_sums (list)`: List of sets for tracking seen values per column.
- `columns_to_test (list, optional)`: Columns to validate for uniqueness.

#### Raises
- `ValueError`: If duplicate values are detected.

### `check_no_nulls`
Validates that specified columns do not contain null or empty values.

#### Parameters
- `idx` (int): Row number.
- `row` (list): List of values in the row.
- `header` (list): List of column names.
- `column_sums` (list): (Unused) Placeholder for memory storage.
- `columns_to_test` (list, optional): Columns to check for null values.

#### Raises
- `ValueError`: If null values are found.

### `check_numeric_range`
Ensures numeric values in specified columns fall within a defined range. Allows null values.

#### Parameters
- `idx` (int): Row number.
- `row` (list): List of values in the row.
- `header` (list): List of column names.
- `column_sums` (list): (Unused) Placeholder for memory storage.
- `columns_to_test` (list, optional): Columns to check for numeric range.
- `min_value` (int|float, optional): Minimum allowed value.
- `max_value` (int|float, optional): Maximum allowed value.

#### Raises
- `ValueError`: If values fall outside the specified range.

### `check_string_pattern`
Validates that values in specified columns match a given regex pattern. Allows null values.

#### Parameters
- `idx` (int): Row number.
- `row` (list): List of values in the row.
- `header` (list): List of column names.
- `column_sums` (list): (Unused) Placeholder for memory storage.
- `columns_to_test` (list, optional): Columns to validate.
- `regex_pattern` (str): Regular expression to match.

#### Raises
- `ValueError`: If values do not match the regex pattern.

### `check_date_format`
Ensures dates in specified columns match a given date format. Allows null values.

#### Parameters
- `idx` (int): Row number.
- `row` (list): List of values in the row.
- `header` (list): List of column names.
- `column_sums` (list): (Unused) Placeholder for memory storage.
- `columns_to_test` (list, optional): Columns to validate.
- `date_format` (str): Expected date format (default: `%Y-%m-%d`).

#### Raises
- `ValueError`: If values do not match the date format.


### `check_datatype`
Validates that values in specified columns match the expected datatype. Allows null values.

#### Parameters
- `idx` (int): Row number.
- `row` (list): List of values in the row.
- `header` (list): List of column names.
- `column_sums` (list): (Unused) Placeholder for memory storage.
- `columns_to_test` (list, optional): Columns to validate.
- `expected_datatype` (type): Expected datatype (e.g., `int`, `float`).

#### Raises
- `ValueError`: If values do not match the expected datatype.

### `check_in_set`
Ensures values in specified columns are within a predefined set.

#### Parameters
- `idx` (int): Row number.
- `row` (list): List of values in the row.
- `header` (list): List of column names.
- `column_sums` (list): (Unused) Placeholder for memory storage.
- `columns_to_test` (list, optional): Columns to validate.
- `valid_values_set` (list): Allowed values for validation.

#### Raises
- `ValueError`: If values are not in the allowed set.
