---
title: Numeric Utilities Documentation
linkTitle: Numeric
weight: 3
prev: /bigquery-utils/modules/utils/custom-data-checks
next: /bigquery-utils/modules/utils/string
cascade:
  type: docs
---

## Introduction

This module provides a set of utility functions for numeric variables. The `Numeric` class simplifies operations involving numeric conversions, particularly in the context of byte size transformations into human-readable units.


## Class Initialization
To use the `Numeric` utilities, you need to create an instance of the class:

```python
numeric_utils = Numeric()
```

The `Numeric` class does not require any parameters during initialization. Once instantiated, you can call its methods for various numeric conversions.

## Methods Overview
### `convert_bytes_to_unit`
#### Description  
Converts a number of bytes into a specified unit (e.g., KB, MB, GB, TB).

#### Parameters
- `byte_count` (int): The number of bytes to convert.
- `unit` (str): The target unit. Supported values are `"KB"`, `"MB"`, `"GB"`, `"TB"`.

#### Returns
- `float`: The byte count converted to the specified unit.

#### Raises
- `ValueError`: If an unsupported unit is provided.

#### Example
```python
numeric_utils = Numeric()

try:
    size_in_gb = numeric_utils.convert_bytes_to_unit(1073741824, "GB")
    print(size_in_gb)  # Output: 1.0
except ValueError as e:
    print(f"Error: {e}")
```
