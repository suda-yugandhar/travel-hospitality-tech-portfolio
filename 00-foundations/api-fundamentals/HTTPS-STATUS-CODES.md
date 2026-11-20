| Code | Meaning | Hotel API example |
|---|---|---|
| 200 | OK | Room availability retrieved |
| 201 | Created | Booking successfully created |
| 202 | Accepted | Booking request accepted for processing |
| 204 | No Content | Booking deleted successfully; no response body |
| 301 | Moved Permanently | API endpoint permanently redirected |
| 302 | Found | Temporary redirect |
| 400 | Bad Request | Invalid booking information |
| 401 | Unauthorized | Missing or invalid authentication |
| 403 | Forbidden | User lacks permission |
| 404 | Not Found | Booking ID does not exist |
| 405 | Method Not Allowed | POST used on a GET-only endpoint |
| 409 | Conflict | Booking conflicts with existing inventory |
| 415 | Unsupported Media Type | Unsupported request format |
| 422 | Unprocessable Content | Request understood but business validation failed |
| 429 | Too Many Requests | API rate limit exceeded |
| 500 | Internal Server Error | Server encountered an unexpected error |
| 502 | Bad Gateway | Upstream server returned an invalid response |
| 503 | Service Unavailable | Booking service temporarily unavailable |
| 504 | Gateway Timeout | Upstream service did not respond in time |
