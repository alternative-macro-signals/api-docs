# `/nipi` Query News Inflationary Pressures Indices Databases: NIPI, NVI, Entropy 
   [![API Status](https://img.shields.io/badge/API-Live-brightgreen)](https://alt.ms/status)

[![Method](https://img.shields.io/badge/Method-GET-blue)](#)

[![Endpoint](https://img.shields.io/badge/Endpoint-%2Fnbstat-important)](#)
[![Authentication](https://img.shields.io/badge/Auth-Bearer%20Token-blue)](../authentication.md)
[![Secure](https://img.shields.io/badge/Security-HTTPS-2EA44F)](../authentication.md)




## 📌 Overview 

The `/nipi` endpoint provides access to the News Inflationary Pressures Indices, a daily diffusion index showing the balance of positive and negative short-term inflation news. 

The `/nipi` endpoint provides access to the [NIPI databases](https://alt.ms/nipi), providing daily inflation news
measures for 23 countries.

The `/nipi` endpoint represents the current data vintage. Small data revisions can happen within a 48 hours window. 
To access vintages (point-in-time snapshots) of the data, please use the /nipipoi endpoint [forthcoming].


The reported indices fluctuate around 50 which is reached when the volume of positive and negative news are equal. A NIPI index value above (below) 50 suggests near-term inflation is about to increase (decrease). 


broadly similar to our [Real-time NewsBot app](https://nb-data.alternativemacrosignals.com/), with a few additional features.

## Authentication

Requires Bearer token authentication. [See Authentication](../authentication.md).

## 🗒️ Query Parameters 


All parameters are optional.

| Parameter | Type   | Description                           | Default      | Accepted values                                                                       |
|-----------|--------|---------------------------------------|--------------|---------------------------------------------------------------------------------------|
| location  | string | Country name                          | `Global23`   | Country name, see supported list below                                                |
| start     | string | Start date (ISO format: YYYY-MM-DD)   | 180 days ago | Any date since `2018-01-01`                                                           |
| end       | string | End date (ISO format: YYYY-MM-DD)     | Yesterday    | Any date since `2018-01-02`                                                           |
| sector    | string | NIPI sector                           | `Headline`    | `Headline`, `Core`, `Telecom`,`Food`, `Energy`,<br/>`Wages`, `All`. See detail below. |


### Supported Locations

#### North America:
- `Canada`
- `Mexico`
- `US`


#### South America:
- `Argentina`
- `Chile`
- `Colombia`
- `Peru`



#### Euro area countries
- `Austria`
- `France`
- `Germany`
- `Ireland`
- `Italy`
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
- `India`
- `Japan`
- `Malaysia`
- `Philippines`

#### Africa
- `Nigeria`
- `South Africa`

#### Global and regional aggregates
- `Euro area` (unweighted news from euro area countries)
- `Global23` (country-weighted news from all above countries)
- `all` (unweighted news from all above countries)

### Sector detals

The `sector` parameter supports the following **Inflation** (consumer prices) measures.

- `Headline`: headline inflation
- `Core`: inflation excluding food and energy
- `Telecom`: telecom services 
- `Food`: food inflation 
- `Energy`: energy and other utilities (e.g. water)

In addition, the following two sectors are included:
- `Wages`: wage related news (e.g. news on minimum wage changes or wage negotiations round)
- `All`: combined wage and inflation measure (i.e. `Headline` and `Wages` news)


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

