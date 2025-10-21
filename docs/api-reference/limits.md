# Rate limits

[![Rate Limits](https://img.shields.io/badge/Rate%20Limits-Strict-red)](docs/api-reference/rate-limits.md)

Make sure your usage does not exceed the following limits (number of requests / time period):

## /token endpoint
* 10 / 5min

## other endpoints
* 60 / 1min


## Note

* These limits are subject to change without notice


* More favourable limits cannot be granted


* Authentication failures will trigger lower limits


## 📋 Best Practices 


* When querying multiple time series, do NOT request a token for each time series. 
You can use the same token for multiple requests, tokens normally last 1 hour. 

----------------

➡️ [Home](../../README.md)


➡️ API [Endpoints](endpoints/endpoints.md) 




