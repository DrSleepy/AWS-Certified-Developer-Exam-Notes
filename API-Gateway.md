# API-Gateway

API-Gateway is used to managed APIs

1. Has caching capabilities to increase performance
2. Is low cost and scales automatically
3. Can throttle API Gateway to prevent attacks
4. Log results to CloudWatch
5. Enable CORS on API Gateway if using multiple domains
6. CORS is enforced by the client
7. Can be used to import an API from a Swagger file
8. Default throttle rate is 10,000 requests **per second** - can be changed but will incur fee
9. Default **concurrent** (at the same millisecond) requests is 5,000 - can be changed but will incur fee
10. Throws error 429 (Too Many Requests) if requests exceed either throttle rates
11. Can be used for SOAP API architecture
