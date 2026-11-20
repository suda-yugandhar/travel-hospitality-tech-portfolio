**HTTPS STATUS CODES:**
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


**HTTPS STATUS CODES 4 MMAJOR CATEGORIES**
| Category | Range | Meaning |
|---|---|---|
| 1xx | 100–199 | Informational |
| 2xx | 200–299 | Successful |
| 3xx | 300–399 | Redirection |
| 4xx | 400–499 | Client-side request issues |
| 5xx | 500–599 | Server-side issues |


**Product Manager insight:**
Suppose a hotel's booking conversion suddenly drops.

Your engineering team reports:
- 401 errors increased by 30%.
- 429 errors increased by 20%.
- 500 errors increased by 10%.
That means we investigate three different possibilities:
1. Authentication problems.
2. API rate limits.
3. Server reliability.
These are different problems requiring different solutions.



**HTTP Headers**
Headers carry additional information about a request or response.
Think of them as instructions and metadata accompanying the request.

| Header | Purpose | Example |
|---|---|---|
| Content-Type | Format of the request body | `application/json` |
| Accept | Response format the client accepts | `application/json` |
| Authorization | Authentication credentials | `Bearer <token>` |
| Cache-Control | Caching instructions | `no-cache` |
| User-Agent | Identifies the requesting application | `HotelBookingApp/1.0` |
| Location | Identifies a resource location, often after creation | `/v1/bookings/1024` |
| Idempotency-Key | Helps prevent duplicate operations | `booking-abc-123` |
| X-Correlation-ID | Helps trace requests across systems | `req-12345` |

**Example HTTP request*
POST /v1/bookings HTTP/1.1
Host: api.example.com
Content-Type: application/json
Accept: application/json
Authorization: Bearer YOUR_ACCESS_TOKEN
Idempotency-Key: booking-abc-123

The server understands:
- The client wants to create a booking.
- The request body is JSON.
- The client expects a JSON response.
- Authentication credentials are provided.
- A unique key is supplied to help prevent duplicate processing.

**Security note**: Never expose actual API keys, access tokens or passwords in a public GitHub repository.

**REST API Conventions**
| Poor convention | Better REST convention |
|---|---|
| `/getRooms` | `/rooms` |
| `/createBooking` | `/bookings` |
| `/deleteBooking/1024` | `/bookings/1024` |
| `/getGuestDetails/55` | `/guests/55` |
| `/updateRoom/12` | `/rooms/12` |

It is an architectural style for designing networked applications.
The most important principle to understand initially is that REST APIs generally expose resources and use HTTP methods to operate on those resources.



**REST conventions you should follow**
**1. Use nouns for resources**

Prefer:
- /guests
- /bookings
- /rooms
- /payments


**2. Use plural resource names
**
Prefer /bookings instead of /booking.

**3. Use IDs for individual resources
**
GET /v1/bookings/1024

**4. Use query parameters for filtering**
GET /v1/rooms?type=deluxe&available=true

**5. Use pagination for large datasets**
GET /v1/bookings?page=1&limit=20

**6. Version your APIs**
/v1/bookings


**ZERO DOWN:**
Imagine we're developing our Hotel Connectivity Simulator.

A hotel uses a Property Management System (PMS), and an external booking platform wants to retrieve room availability.

The booking platform sends:
GET /v1/rooms/availability?check_in=2026-12-10&check_out=2026-12-15

The API responds:
HTTP/1.1 200 OK
Content-Type: application/json

Response body:
{
  "hotel_id": "HTL001",
  "check_in": "2026-12-10",
  "check_out": "2026-12-15",
  "available_rooms": [
    {
      "room_type": "Deluxe",
      "available": 5,
      "price_per_night": 150
    },
    {
      "room_type": "Suite",
      "available": 2,
      "price_per_night": 280
    }
  ],
  "currency": "EUR"
}

Now imagine the booking platform tries to retrieve availability but sends an invalid date.

The API could respond:
HTTP/1.1 400 Bad Request
Content-Type: application/json

{
  "error": "INVALID_DATE",
  "message": "Check-out date must be later than check-in date."
}

This is what API integration looks like in practice.
/v2/bookings

This helps manage changes without unexpectedly breaking existing integrations.
