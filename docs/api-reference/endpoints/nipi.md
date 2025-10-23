# `/nipi` Query News Inflationary Pressures Indices Databases: NIPI, NVI, Entropy 
   [![API Status](https://img.shields.io/badge/API-Live-brightgreen)](https://alt.ms/status)

[![Method](https://img.shields.io/badge/Method-GET-blue)](#)

[![Endpoint](https://img.shields.io/badge/Endpoint-%2Fnipi-important)](#)
[![Authentication](https://img.shields.io/badge/Auth-Bearer%20Token-blue)](../authentication.md)
[![Secure](https://img.shields.io/badge/Security-HTTPS-2EA44F)](../authentication.md)




## 📌 Overview 

The `/nipi` endpoint provides access to the [News Inflationary Pressures Indices](https://alt.ms/nipi), a daily diffusion index showing the balance of positive and negative short-term inflation news. 

The reported indices fluctuate around 50 which is reached when the volume of positive and negative news are equal. 

A NIPI index value above (below) 50 suggests near-term inflation is about to increase (decrease). 

The NIPI aggregates news over the a 30-days rolling period.

The data accessible through the `/nipi` endpoint is the current data vintage. Small data revisions can happen within a 48 hours window. 
Vintages (point-in-time snapshots) of the data will be available in the future through the `/nipipoi` endpoint.

Can be called directly from our [Python SDK](../../sdk/python/ams-sdk.md).

## Authentication

Requires Bearer token authentication. [See Authentication](authentication.md). 

## 🗒️ Query Parameters 


All parameters are optional.

| Parameter | Type                       | Description                         | Default      | Accepted values                                                                                                                                                       |
|-----------|----------------------------|-------------------------------------|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| location  | string or list of strings  | Country name                        | `Global23`   | See supported location below <br/>`["US", "Canada"]` to query for both Canada and US NIPI data. <br/>`*` to download all available locations, including region aggregates. |
| start     | string                     | Start date (ISO format: YYYY-MM-DD) | 180 days ago | Any date since `2018-01-01`                                                                                                                                           |
| end       | string                     | End date (ISO format: YYYY-MM-DD)   | Yesterday    | Any date since `2018-01-02`                                                                                                                                           |
| sector    | string  or list of strings | NIPI sector                         | `Headline`   | `Headline`, `Core`, `Telecom`,`Food`, `Energy`,<br/>`Wages`, `All`<br/> lists, eg `["Core","Food"]`                                                                   |
| metric    | string                     | NIPI or NVI                         | `NIPI`       | `NIPI`, `NVI`                                                                                                                                                         |


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
- `EA`: Euro area proxy = four largest euro area countries country-weighted (Germany, France, Italy and Spain)
- `Global23`:  all currently covered countries country-weighted
- `all`: unweighted news from all above countries

Note: country weights are detailed below.

### Sectors

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
           'sector': 'Core' } 
headers = {'Authorization': f'Bearer {token}'} 
response = requests.get(f'{SERVICE_URL}/nipi', 
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

| Field     | Type   | Description                               |
|-----------|--------|-------------------------------------------|
| date      | string | Observation date, end of day (ISO format) |
| value     | float  | NIPI value for the day                    |
| meta      | dict   | Metadata                                  |





### NIPI computation


On a given day:

$$
NIPI^* = (((entr_+ - entr_-) / S ) + 1 ) * 50 
$$

for a given country, sector 

$entr_+$ measures are the sum of probability of news being positive (when proba > 0.60) and
$entr_-$ the sum of probability of news being negative (when proba > 0.60).




S is a constant which is country, sector specific defined as: S = max(3, Q). Q is the 0.90 quantile value of the total number of news (relevant news, whatever their sign) series range over the period 1/1/18-31/12/2020. The pandas dataframe function used is df.quantile(q=0.9, interpolation="higher").

The NIPI is the unweighted average of the last 30 daily NIPI* observations.


### Country weights

#### `Global23` aggregate
* Argentina: 0.0113
* Australia: 0.0149
* Austria: 0.0056
* Canada: 0.0212
* Chile: 0.0053
* China: 0.2675
* Colombia: 0.0085
* France: 0.0349
* Germany: 0.0511
* India: 0.1076
* Ireland: 0.0055
* Italy: 0.0289
* Japan: 0.0596
* Malaysia: 0.0103
* Mexico: 0.0289
* Nigeria: 0.0118
* Peru: 0.0048
* Philippines: 0.0107
* South Africa: 0.0091
* Spain: 0.0212
* Switzerland: 0.0070
* UK: 0.0351
* US: 0.2391

#### `Euro area` aggregate

* France: 0.265 
* Germany: 0.382 
* Italy: 0.215 
* Spain: 0.138 

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

