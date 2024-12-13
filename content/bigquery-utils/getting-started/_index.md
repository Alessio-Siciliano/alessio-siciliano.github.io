---
title: Getting Started
weight: 1
next: /bigquery-utils/modules
prev: /bigquery-utils
cascade:
  type: docs
---

## Quick Start

{{< icon "github" >}}&nbsp;[Alessio-Siciliano/bigquery-advanced-utils](https://github.com/Alessio-Siciliano/bigquery-advanced-utils)

You can quickly get started by installing the package with pip:

```shell
pip install bigquery-advanced-utils
```

## Start as New Project

### Prerequisites

Before starting, you need to have the following software installed:

- [Python](https://python.org/)
- [Git](https://git-scm.com/) (*optional*)

### Steps

{{% steps %}}

### Create a new virtual environment

```shell
python -m venv venv
```

### Activate the new environment

```shell
source venv/bin/activate  # on macOS/Linux  
venv\Scripts\activate     # on Windows  
```

### Install the package

Install the latest version available with the package manager PIP:

```shell
pip install bigquery-advanced-utils
```

### Import classes in your code

Now, you can import all the classes from "bigquery_advanced_utils" as:
```python
from bigquery_advanced_utils.bigquery import BigQueryClient
```

{{% /steps %}}


{{% details title="How to update the package with the future versions?" %}}

To update the package in your project to its latest versions, run the following command:

```shell
pip install --upgrade bigquery-advanced-utils
```
{{% /details %}}

<!--## Next

Explore the following sections for more information about the package:

{{< cards >}}
  {{< card link="../guide/organize-files" title="Organize Files" icon="document-duplicate" >}}
  {{< card link="../guide/configuration" title="Configuration" icon="adjustments" >}}
  {{< card link="../guide/markdown" title="Markdown" icon="markdown" >}}
{{< /cards >}}-->