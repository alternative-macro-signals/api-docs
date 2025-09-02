# Authentication `/token`

[![API Status](https://img.shields.io/badge/API-Live-brightgreen)](https://alt.ms/status)

[![Method](https://img.shields.io/badge/Method-POST-blue)](#)

[![Authentication](https://img.shields.io/badge/Auth-Required-red)](../authentication.md)
[![Token Auth](https://img.shields.io/badge/Auth-Bearer%20Token-blue)](../authentication.md)
[![Secure](https://img.shields.io/badge/Security-HTTPS-2EA44F)](../authentication.md)


## 📌 Overview  

The Alternative Macro Signals API uses a two-step authentication:

① API Key authentication to obtain a temporary access token


② Bearer token authentication for subsequent requests

Your API key should be kept secure and never shared or committed to version control.


## 🔐 API Key 

If you haven't got a key already or if you lost it, contact [support@alternativemacrosignals.com](mailto:support@alternativemacrosignals.com) to obtain a new key. 

In addition to your API key, you will be given the `SERVICE_URL`.

The API is restricted to AMS customers with programmatic access.

If you are a customer without programmatic access to the data or if you would like to get first hand experience with our data, 
 trial access can be requested.

## 🎟 Access Token 

### Endpoint: POST `/token`

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

The token is valid 1 hour.


### ❌ Error Responses

| Status Code | Description             |
|-------------|-------------------------|
| 401         | Invalid / no API key    |
| 403         | API key not enabled     |
| 429         | Too many token requests |

## 🟢 Using the Token 

Include the token in all subsequent API requests using the Authorization header:

```python
headers = {"Authorization": f"Bearer {token}"}
```
## 🛡️ Security Best Practices 

1. Never share or expose your API key
2. Use environment variables for API keys
3. Don't hardcode tokens in your application
4. Rotate tokens regularly
5. Request new tokens when expired

----------
➡️ [Home](../../../README.md)

➡️ API [Endpoints](docs/api-reference/endpoints/endpoints.md) 

