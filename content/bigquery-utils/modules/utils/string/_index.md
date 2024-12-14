---
title: String Manipulation Utilities Documentation
linkTitle: String
weight: 4
prev: /bigquery-utils/modules/utils/numeric
cascade:
  type: docs
---

## Introduction

This Python module provides a set of utility functions to manipulate strings, making it easier to handle text processing tasks such as cleaning strings, removing comments, and extracting tables from queries. These utilities are part of the `bigquery-advanced-utils` package and aim to simplify text processing in data workflows.

## Class Initialization

To use the `String` utilities, you first need to create an instance of the class:

```python
from bigquery_advanced_utils.utils.string import String

string_utils = String()
```

The `String` class does not require any parameters during initialization. Once instantiated, you can call its methods for various string manipulation tasks.

## Methods Overview
### `remove_chars_from_string`

#### Description  
Removes specific characters from a given string.

#### Parameters
- `string` (str): The input string to process.
- `chars_to_remove` (list[str]): A list of characters to remove from the input string.

#### Returns
- `str`: A new string with the specified characters removed.

#### Raises
- `InvalidArgumentToFunction`: If the input parameters are invalid (e.g., `string` is `None`, or `chars_to_remove` is not a non-empty list).

#### Example
```python
from bigquery_advanced_utils.utils.string import String

string_utils = String()
input_string = "Hello, World!"
chars_to_remove = [",", "!"]

try:
    cleaned_string = string_utils.remove_chars_from_string(input_string, chars_to_remove)
    print(cleaned_string)  # Output: "Hello World"
except InvalidArgumentToFunction:
    print("Invalid arguments provided to the function.")
```


### `remove_comments_from_string`

#### Description  
Removes all comments from a given string based on the specified dialect (default is `standard_sql`).

#### Parameters
- `string` (str): The input string, typically a SQL query.
- `dialect` (str): The dialect to use for identifying comments. Default is `standard_sql`.

#### Returns
- `str`: The string with all comments removed.

#### Raises
- `InvalidArgumentToFunction`: If the input parameters are invalid (e.g., `string` is `None`).

#### Example
```python
input_query = """SELECT * FROM table -- This is a comment
WHERE id = 1;"""

try:
    cleaned_query = string_utils.remove_comments_from_string(input_query)
    print(cleaned_query)  # Output: "SELECT * FROM table WHERE id = 1;"
except InvalidArgumentToFunction:
    print("Invalid arguments provided to the function.")
```

### `extract_tables_from_query`

#### Description
Extracts all table names from a SQL query string.

#### Parameters
- `string` (str): The input SQL query string.

#### Returns
- `list[str]`: A list of unique table names extracted from the query.

#### Raises
- `InvalidArgumentToFunction`: If the input string is `None`.

#### Example:
```python
query = """SELECT * FROM `project.dataset.table` JOIN `project.dataset.table2` ON id = id
-- Commented out code
WHERE condition;"""

try:
    tables = string_utils.extract_tables_from_query(query)
    print(tables)  # Output: ["project.dataset.table", "project.dataset.table2"]
except InvalidArgumentToFunction:
    print("Invalid arguments provided to the function.")
