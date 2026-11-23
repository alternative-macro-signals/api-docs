# `/newsbot` Download the daily NewsBot editions
   [![API Status](https://img.shields.io/badge/API-Live-brightgreen)](https://alt.ms/status)

[![Method](https://img.shields.io/badge/Method-GET-blue)](#)

[![Endpoint](https://img.shields.io/badge/Endpoint-%2Fnewsbot-important)](#)
[![Authentication](https://img.shields.io/badge/Auth-Bearer%20Token-blue)](../authentication.md)
[![Secure](https://img.shields.io/badge/Security-HTTPS-2EA44F)](../authentication.md)




## 📌 Overview

The `/newsbot` endpoint serves the daily NewsBot editions as JSON: the same
curated selection of inflation (and wages) news our subscribers receive by
email, with semantic grouping, translation and region ordering already applied.

Each edition is a **point-in-time artifact**: it is published once by the
production run and never rebuilt, so what you download is exactly what was
sent. Both the **latest** edition and the full **history** (by date) are
available, as well as a catalogue of all published editions.

Editions are published on **weekdays only**:

- `tz=et`: the London morning edition (early European trading hours)
- `tz=ny`: the New York afternoon edition (`inflation` topic only)

Can be called directly from our [Python SDK](../../sdk/python/ams-sdk.md).

## Authentication

Requires Bearer token authentication. [See Authentication](authentication.md).

Access is granted **per topic**: `inflation` and `wages` are separate
subscriptions. A key entitled to one topic receives `403` on the other.

## 🗒️ Query Parameters


| Parameter | Type   | Description                                      | Default     | Accepted values                                      |
|-----------|--------|--------------------------------------------------|-------------|------------------------------------------------------|
| topic     | string | NewsBot topic                                    | `inflation` | `inflation`, `wages`                                 |
| tz        | string | Edition: London AM (`et`) or New York PM (`ny`)  | required    | `inflation`: `et`, `ny` — `wages`: `et` only         |
| date      | string | Edition day (ISO format: YYYY-MM-DD)             | latest      | Any published weekday (see `index`)                  |
| index     | string | `index=1` lists all published editions (metadata only, no news content) | off | `1` |

With `index=1`, `tz` and `date` are not needed. Unknown parameters, an unknown
`topic`, a `tz` not valid for the topic, or a malformed `date` return `422`.

## Example Request
```python
import requests
params = { 'topic': 'inflation',
           'tz': 'et' }
headers = {'Authorization': f'Bearer {token}'}
response = requests.get(f'{SERVICE_URL}/newsbot',
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
| content   | dict    | The requested edition (or the editions catalogue with `index=1`) |


### Content Fields

One NewsBot edition:

| Field        | Type   | Description                                              |
|--------------|--------|----------------------------------------------------------|
| topic        | string | `inflation` or `wages`                                   |
| tz           | string | `et` (London AM) or `ny` (New York PM)                   |
| day          | string | Edition day (YYYY-MM-DD)                                 |
| release_id   | string | Production release identifier                            |
| releaseTime  | string | Edition build time, e.g. `2026-11-23_08:53_CET`          |
| generated_at | string | Publication timestamp (ISO format, UTC)                  |
| payload      | dict   | The news items (see below)                               |

### Payload Fields

`payload` contains a `releaseTime` field plus one entry per news item, keyed
`"0"`, `"1"`, … as strings. The numbering preserves the curated edition order
(items are grouped by region, most relevant first). Each item:

| Field       | Type   | Description                                                             |
|-------------|--------|-------------------------------------------------------------------------|
| title       | string | Article title (English translation for foreign-language articles)       |
| sum         | string | Article summary (English translation for foreign-language articles)     |
| url         | string | Link to the original article                                            |
| srce        | string | Source / publisher name                                                 |
| publishedAt | string | Article publication time (ISO format)                                   |
| lang        | string | Original article language code (e.g. `en`, `de`)                        |
| loc         | string | Country / location the article refers to (comma-separated when several) |
| region      | string | Regional grouping used to order the edition (e.g. `Advanced`)           |
| sector      | string | Sector classification (`Core`, `Food`, `Energy`; wage news for `wages`) |
| stars       | int    | Relevance rating (higher = more prominent in the edition)               |
| themes      | list   | Theme labels attached to the article (may be empty)                     |

Note: editions published before 2026-06-29 predate the `themes` enrichment and
do not carry the `themes` field.

### Editions catalogue (`index=1`)

With `index=1`, `content` is a list of all published editions for the topic,
newest first, metadata only:

| Field        | Type   | Description                            |
|--------------|--------|----------------------------------------|
| topic        | string | `inflation` or `wages`                 |
| tz           | string | `et` or `ny`                           |
| day          | string | Edition day (YYYY-MM-DD)               |
| release_id   | string | Production release identifier          |
| generated_at | string | Publication timestamp (ISO format, UTC)|

### Error Responses

| Status Code | Description                                                                 |
|-------------|------------------------------------------------------------------------------|
| 401         | Missing, invalid or expired token                                           |
| 403         | Token valid but the key is not entitled to the requested `topic`            |
| 404         | No edition published for the given `topic`/`tz`/`date` (e.g. a weekend day) |
| 422         | Unexpected parameter, unknown `topic`, `tz` not valid for the topic, or invalid `date` |
| 429         | Rate limit exceeded                                                         |

---------------
➡️ [Home](../../../README.md)


➡️ API [Endpoints](endpoints.md)
