# `/nbstat` Query News Stats 

   [![API Status](https://img.shields.io/badge/API-Live-brightgreen)](https://alt.ms/status)

[![Method](https://img.shields.io/badge/Method-GET-blue)](#)

[![Endpoint](https://img.shields.io/badge/Endpoint-%2Fnbstat-important)](#)
[![Authentication](https://img.shields.io/badge/Auth-Bearer%20Token-blue)](../authentication.md)
[![Secure](https://img.shields.io/badge/Security-HTTPS-2EA44F)](../authentication.md)




## 📌 Overview 
The `/nbstat` endpoint provides aggregated news statistics. The user can define a query for specific inflation news,
including specifying a text search and the location, and will get in return detailed inflation metrics for the specific query.    

Three main metrics are provided:
- Daily balance score, $B_t$
- Daily inflation news sign, $S_t$
- Daily news volume, $V_t$

The data is similar to AMS NewsBot app, with a extended coverage (daily data without smoothing and extended history).

Can be called directly from our [Python SDK](../../sdk/python/ams-sdk.md).

## Authentication

Requires Bearer token authentication. [See Authentication](authentication.md).

## 🗒️ Query Parameters 


All parameters are optional.

| Parameter | Type   | Description                           | Default         | Accepted values                        |
|-----------|--------|---------------------------------------|-----------------|----------------------------------------|
| location  | string | Country name                          | None            | Country name, see supported list below |
| start     | string | Start date (ISO format: YYYY-MM-DD)   | 180 days ago    | Any date since `2020-01-01`            |
| end       | string | End date (ISO format: YYYY-MM-DD)     | Yesterday       | Any date since `2020-01-01`            |
| txt       | string | Text search with logical operators    | None            | See syntax below                       |
| sector    | string | CPI sub-component                     | None (Headline) | `Core`, `Food` or `Energy`             |
| sign      | string | Inflation sign filter                 | None (all)      | `Positive`, `Neutral`, `Negative`      |
 | minrating | string | Minimum relevance rating, from 0 to 5 | 0               | `0`, `1`, `2`, `3`, `4`,`5`            |


### Supported Locations

#### North America:
- `Canada`
- `US`

#### Euro area
 - `Austria`
- `Belgium`
- `Euro area`
- `Finland`
- `France`
- `Italy`
- `Germany`
- `Greece`
- `Ireland`
- `Netherlands`
- `Portugal`
- `Slovakia`
- `Spain`

Note: `Euro area` aggregates all euro area countries without country weight.

#### Non-euro area Europe
- `Denmark`
- `Norway`
- `Sweden`
- `Switzerland`
- `UK` 

#### Asia and Oceania
- `Australia` 
- `China`
- `Japan`
- `New Zealand`


### Text Search Syntax

The `txt` parameter supports:
- Simple search: `"car insurance"`
- OR operator: `"car OR auto"`
- AND operator: `"car AND insurance"`
- NOT operator: `"insurance NOT car"`
- Multiple exclusions: `"insurance NOT car home house"`


Notes:
- One logical operator per expression
- S-plural forms are automatically included (e.g "cars" with "car")
- Operators must be uppercase
- Keywords are case-insensitive

## Example Request
```python
import requests
params = { 'location': 'US', 
           'start': '2025-01-01', 
           'txt': 'insurance NOT car' } 
headers = {'Authorization': f'Bearer {token}'} 
response = requests.get(f'{SERVICE_URL}/nbstat', 
                        headers=headers, 
                        params=params)
```
See also our [Python SDK](../../sdk/python/ams-sdk.md).

## Response

### Response Fields

| Field     | Type    | Description                       |
|-----------|---------|-----------------------------------|
| datetime  | string  | Request date (ISO format)         |
| status    | string  | Request status, 200 if successful |
| content   | list    | Requested data                    |


### Content Fields
Each line of data in "content" gathers metrics for 1 day in a dictionary form, with the following fields:

| Field      | Type    | Description                               |
|------------|---------|-------------------------------------------|
| date       | string  | Observation date, end of day (ISO format) |
| sign_daily | float   | Daily inflation news sign (-1 to 1)       |
| vol_daily  | integer | Daily news volume                         |
| bal_daily  | float   | Daily balance score                       |

### Detailed metrics

The daily news volume, $V_t$ hereafter, is the number of inflation news observed on day *t*.

The daily inflation news sign, or $S_t$, is defined as:

$$
S_t = \frac{\sum_{i=1}^{n} \rho^+_{i,t} - \sum_{i=1}^{n} \rho^-_{i,t}}{V_{t}}
$$

where
$\rho^+_{i,t}$ is the probability of news i to be positive for inflation on the day, 
and $\rho^-_{i,t}$ the probability of news i to be negative for inflation.

$S_t$ is therefore the difference between the sum of positive probabilities and the sum of negative probabilities, 
divided by the total number of news. It is therefore bound by -1 and 1.

Finally, the daily balance score is defined as:

$$B_t = V_t * S_t = \sum_{i=1}^{n} \rho^+_{i,t} - \sum_{i=1}^{n} \rho^-_{i,t}$$

Of the three, the daily balance is the closest to our NIPI metric (though not exactly identical).

### Error Responses

| Status Code | Description              |
|-------------|--------------------------|
| 400         | Invalid parameters       |
| 401         | Invalid or expired token |
| 422         | Unexpected parameter     |
| 429         | Rate limit exceeded      |

---------------
➡️ [Home](../../../README.md)


➡️ API [Endpoints](docs/api-reference/endpoints/endpoints.md) 

