# Alternative Macro Signals API Documentation

Welcome to the official documentation for the Alternative Macro Signals (AMS) API. This repository contains comprehensive documentation and examples for integrating with our macroeconomic data service.

[![API Status](https://img.shields.io/badge/API-Live-green)](https://alt.ms/status)
[![Documentation](https://img.shields.io/badge/docs-up--to--date-brightgreen)](https://docs.alt.ms)

## 🚀 Quick Start++

Get news statistics for the US market in just a few lines:

```python
import requests
```
### Get access token

```python
SERVICE_URL = "<service_url>" # Provided upon registration 
headers = {'X-API-Key': 'your-api-key'} 
token = requests.post(f'{SERVICE_URL}/token', headers=headers).json()
```
Both service URL and API key to be provided upon service registration. 

### Query inflation news statistics

To query news statistics (News Balance) associated with "insurance" news, in the US:
```python
params = {'location': 'US', 'txt': "insurance"} 
headers = {'Authorization': f'Bearer {token}'}
response = requests.get(f'{SERVICE_URL}/nbstat', headers=headers, params=params)
print(response.json()[0]) # Latest news statistics
```
will return XX




## 📚 Documentation

<!--
### Getting Started
- [Authentication and API Keys](docs/getting-started/authentication.md)
- [Quick Start Guide](docs/getting-started/quickstart.md)
- [Installation Instructions](docs/getting-started/installation.md)
-->


### API Reference
- Endpoints
  - [Authentication (/token)](docs/api-reference/endpoints/authentication.md)
  - [News Statistics (/nbstat)](docs/api-reference/endpoints/nbstat.md)
- [Error Handling](docs/api-reference/errors.md)
- [Rate Limits](docs/api-reference/rate-limits.md)

### Guides & Tutorials
- [Best Practices](docs/guides/best-practices.md)
- [Common Use Cases](docs/guides/common-use-cases.md)

### Code Examples
- [Python Examples](examples/python/)
- [cURL Examples](examples/curl/)
- [JavaScript Examples](examples/javascript/)

## 🔑 Authentication

All API endpoints require authentication. You'll need an API key to access our services. 
[Contact our support team](mailto:support@alternativemacrosignals.com) to obtain your API key.

```python
# Example authentication flow
headers = {'X-API-Key': 'your-api-key'}
token = requests.post('https://api.alt.ms/token', headers=headers).json()
```
## 📊 Available Endpoints
Our API provides access to various macroeconomic data endpoints:
- - Authentication endpoint `/token`
- - News Volumes and News Balances `/nbstat`
- `/newssearch` - Query news database
- `/nipi` - Query NIPI time series

For detailed information about each endpoint, please refer to our [API Reference](docs/api-reference/).
## 💡 Support
- Email: support@alternativemacrosignals.com
- [Submit an Issue](https://github.com/alternative-macro-signals/api-docs/issues)
- [API Status Page](https://alt.ms/status)

## 📅 Changelog
See our [CHANGELOG.md](CHANGELOG.md) for a list of changes and updates to our API.
## 📝 License
This documentation is licensed under [MIT License](LICENSE).
## 🤝 Contributing
We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.
© 2025 Alternative Macro Signals. All rights reserved.
