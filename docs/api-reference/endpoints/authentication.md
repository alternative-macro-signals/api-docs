# Authentication

## Overview

The Alternative Macro Signals API uses a two-step authentication:
1. API Key authentication to obtain a temporary access token
2. Bearer token authentication for subsequent requests

Your API key should be kept secure and never shared or committed to version control.

## API Key

Contact [support@alternativemacrosignals.com](mailto:support@alternativemacrosignals.com) to obtain your API key. You will receive:
- API Key
- Service URL

Access is restricted to customers with programmatic access.

Customers without programmatic access and others can ask for trial access, with some feature restrictions.

## Access Token

### Endpoint: POST /token

Request a temporary access token by presenting your API key.

### Headers

| Name      | Required | Description  |
|-----------|----------|--------------|
| X-API-Key | Yes      | Your API key |

### Example Request
```python
python import requests
SERVICE_URL = "<service_url>" 
headers = {'X-API-Key': 'your-api-key'} 
response = requests.post(f'{SERVICE_URL}/token', headers=headers) 
token = response.json()
```
### Response
String

### Token validity

The token is valid for 1 hour.


### Error Responses

| Status Code | Description             |
|-------------|-------------------------|
| 401         | Invalid / no API key    |
| 403         | API key not enabled     |
| 429         | Too many token requests |

## Using the Token

Include the token in all subsequent API requests using the Authorization header:

```python
headers = {"Authorization": f"Bearer {token}"}
```
## Security Best Practices

1. Never share or expose your API key
2. Use environment variables for API keys
3. Don't hardcode tokens in your application
4. Rotate tokens regularly
5. Request new tokens when expired

