<h1 align="center">
    Alternative Macro Signals API
</h1>
<h3 align="center">
 Macroeconomic data, generated from web scraping and Large Language Models 
</h3>

[AMS](https://alt.ms) derives macroeconomic signals from scanning the web. 
We train Language Models to look for and digest news the way an experienced analyst would.
Our main applications cover daily inflation data and commodities.

[Reach out](https://alt.ms/contact) if you would like to know more.
 
## 🚀 Quick Start

Get the inflation signals from insurance prices in the US, with these few lines: 

### Obtain access token

```python
import requests
```

```python
SERVICE_URL = "<service_url>" # Provided upon registration 
headers = {'X-API-Key': 'your-api-key'} 
token = requests.post(f'{SERVICE_URL}/token', headers=headers).json()
```
Both service URL and API key to be provided upon service registration. 

### Query inflation news statistics

To query news statistics (e.g. the News Balance) associated with "insurance" news, in the US:
```python
params = {'location': 'US', 'txt': "insurance"} 
headers = {'Authorization': f'Bearer {token}'}
response = requests.get(f'{SERVICE_URL}/nbstat', headers=headers, params=params)
print(response.json()[0]) # Latest news statistics
```
will return News Sign, News Volume and Balance. 




## 📚 Documentation

<!--
### Getting Started
- [Authentication and API Keys](docs/getting-started/authentication.md)
- [Quick Start Guide](docs/getting-started/quickstart.md)
- [Installation Instructions](docs/getting-started/installation.md)
-->


### API reference
- [Endpoints](docs/api-reference/endpoints/endpoints.md)
  - [Authentication (/token)](docs/api-reference/endpoints/authentication.md)
  - [News Statistics (/nbstat)](docs/api-reference/endpoints/nbstat.md)
- [Rate Limits](docs/api-reference/limits.md)

### Guides & Tutorials
- [Common Use Cases](docs/guides/common-use-cases.md)


## 💡 Contact
- Support: [support@alternativemacrosignals.com](mailto:support@alternativemacrosignals.com)


- Info: [info@alternativemacrosignals.com](mailto:info@alternativemacrosignals.com)


## 📅 Changelog
See our [CHANGELOG.md](CHANGELOG.md) for a list of changes and updates to our API.


## Author

[Laurent Bilke](https://alt.ms/m/lb)


This documentation is licensed under [MIT License](LICENSE).


© 2025 Alternative Macro Signals. All rights reserved.
