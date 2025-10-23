<h1 >
    Alternative Macro Signals API <img src="./logo_icon_small_tw.jpg" alt="Alternative Macro Signals Logo" width="80"  align="right">
</h1>
<h3 >
 Macroeconomic data, generated from web scraping and Large Language Models 
</h3>

[AMS](https://alt.ms) derives macroeconomic signals from scanning the web. 
We train Language Models to search and analyze news the way an experienced analyst would.
Our main applications cover daily inflation data and commodities.

[Reach out](https://alt.ms/contact) if you would like to know more.
 
## 🚀 Quick Start

Get inflation metrics (balance of inflation news, volume of news, ...) about egg prices in the US, 
using the `nbstat` endpoint.

You'll need: the `SERVICE_URL` and your `API_key`, both delivered by AMS upon registration.

You have two options:

### Option 1: our Python wrapper, [`ams-sdk`](/docs/sdk/python/ams-sdk.md) 
```shell
pip install ams-sdk
```
```python
from ams_sdk.client import AMSClient

client = AMSClient(service_url=SERVICE_URL, api_key=API_KEY)
result = client.query_endpoint("/nbstat", params={"location": "US","txt": "egg"})
```
 

### Option 2: HTTP request methods

Using Python, for instance.

To authenticate:
```python
import requests

headers = {'X-API-Key': API_KEY} 
token = requests.post(f'{SERVICE_URL}/token', headers=headers).json()
```
 
Then use the token for the data quety:
```python
params = {'location': 'US', 'txt': "egg"} 
headers = {'Authorization': f'Bearer {token}'}
response = requests.get(f'{SERVICE_URL}/nbstat', headers=headers, params=params)
```




## 📚 Documentation

<!--
### Getting Started
- [Authentication and API Keys](docs/getting-started/authentication.md)
- [Quick Start Guide](docs/getting-started/quickstart.md)
- [Installation Instructions](docs/getting-started/installation.md)
-->


### API reference
- [Endpoints](docs/api-reference/endpoints/endpoints.md)
  - [Authentication (`/token`)](docs/api-reference/endpoints/authentication.md)
  - [News Statistics (`/nbstat`)](docs/api-reference/endpoints/nbstat.md)
  - [NIPI (`/nipi`)](docs/api-reference/endpoints/nipi.md)
- [Rate Limits](docs/api-reference/limits.md)

### Guides & Tutorials
- [Python SDK](docs/sdk/python/ams-sdk.md)
- [Common Use Cases](docs/guides/common-use-cases.md)


## 💡 Contact
- Support: [support@alternativemacrosignals.com](mailto:support@alternativemacrosignals.com)


- Info: [info@alternativemacrosignals.com](mailto:info@alternativemacrosignals.com)


## 📅 Changelog
See our [CHANGELOG.md](CHANGELOG.md) for a list of changes and updates to our API.


## Author

[Laurent Bilke](https://alt.ms/m/lb)


This documentation is licensed under [MIT License](LICENSE).


© 2025 Alternative Macro Signals. All rights reserved. https://alt.ms <img src="./logo_icon_small_tw.jpg" alt="Alternative Macro Signals Logo" width="30"  align="right">
