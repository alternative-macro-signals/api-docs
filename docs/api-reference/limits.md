# Rate limits

[![Rate Limits](https://img.shields.io/badge/Rate%20Limits-Strict-red)](docs/api-reference/rate-limits.md)

Make sure your usage does not exceed the following limits:

## /token endpoint
* 10 / 5min

## other endpoints
* 60 / 1min


## Note

* These limits are subject to change without notice, in particular in case of elevated traffic to our servers


* More favourable limits cannot be granted


* In case of authentication errors, the limits will be automatically lowered


## 📋 Best Practices 


* If you query multiple time series at a time, do NOT request a token for each time series. Use the same token for multiple requests. 

----------------

➡️ [Home](../../README.md)


➡️ API [Endpoints](docs/api-reference/endpoints/endpoints.md) 




