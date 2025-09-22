# AMS-SDK
![Python Version](https://img.shields.io/badge/Python-3.7%2B-blue)
[![License](https://img.shields.io/badge/License-MIT-yellow)](LICENSE)

`ams-sdk` is a wrapper around `ams-api` and handles the authentification and query process in just a few steps.



Please refer to [AMS API documentation](https://github.com/alternative-macro-signals/api-docs)
 for a detailed description of the API endpoints, including parameters specification.

---

## Features ✨

- **Easy Queries**: Query from all AMS API endpoints in two lines of Python code


- **Authentication**: SDK takes care of the full authentication process, with just your API key required (given by AMS)

---

## Installation 🛠️

From PyPI (recommended):

```shell
pip install ams-sdk
```

Alternatively, directly from repo:

```shell
pip install git+https://github.com/alternative-macro-signals/ams-sdk.git
```

---

## Requirements 📋


The following dependencies are necessary to use this SDK:

- `Python 3.7` or higher (likely to work with 3+ but not tested)
- `requests>=2.0.0` (installed automatically if needed)

---

## Usage 📖


### Initialization
First, initialize the `AMSClient` with the service URL and API key provided by AMS.
```python
from ams_sdk.client import AMSClient
```
```python
client = AMSClient(service_url=SERVICE_URL, api_key=API_KEY)
```

### Authentication

Call the `authenticate()` method to fetch the bearer token required for further requests:

```python
client.authenticate()
```

### Querying Endpoints

Use the `query_endpoint` method to query specific AMS API endpoints:

```python
result = client.query_endpoint("/nbstat", params={
 "location": "Japan",
 "txt": "rice",
 "start": "2021-01-01"
})
print(result)
```



### Output

Transfer the `nbstat` output in a Pandas dataframe:

```python
import pandas as pd
df = pd.DataFrame(result.get('content'))
df['date'] = pd.to_datetime(df['date'])
df = df.set_index('date')
df.sort_index(inplace=True)
```
---
## API endpoints callable from `AMSClient` 🌐


### [`/nbstat`](https://github.com/alternative-macro-signals/api-docs/blob/master/docs/api-reference/endpoints/nbstat.md)
[![API Status](https://img.shields.io/badge/API-Live-brightgreen)](https://github.com/alternative-macro-signals/api-docs/blob/master/docs/api-reference/endpoints/nbstat.md)

Retrieve Inflation News Balance and News Volumes associated with specific text queries.

### /nipi
[![API Status](https://img.shields.io/badge/API-Forthcoming-orange)](#)

Download NIPI data (meanwhile possible from the NIPI app or our CSV files endpoints)


### /inb
[![API Status](https://img.shields.io/badge/API-Forthcoming-orange)](#)

Inflation NewsBot daily lists (meanwhile possible through dedicated JSON endpoints).

----

## We welcome suggestions! 💡

📧: support@alternativemacrosignals.com

---

## Project Structure 📂


- **`client.py`**: Contains the `AMSClient` class which offers the core functionality for interacting with the API.
- **`utils.py`**: `AMSClient` usage examples.
- **`setup.py`**: Handles package configuration and installation details.
- **`README.md`**: Documentation for the `ams-sdk`.

---

## License 📜


This project is licensed under the MIT License. See the [LICENSE](https://github.com/alternative-macro-signals/ams-sdk/blob/main/LICENSE) file for details.


---

## Author

- **Author**: Laurent Bilke - [laurent@alternativemacrosignals.com](mailto:laurent@alternativemacrosignals.com)
- **Repository**: [GitHub](https://github.com/alternative-macro-signals/ams-sdk)

   



---------



© 2025 Alternative Macro Signals. All rights reserved. https://alt.ms <img src="logo_icon_small_tw.jpg" alt="Alternative Macro Signals Logo" width="30"  align="right">
