# API Reference

## Request 
The following API allows the insertion of manifest pre-alert data.

URL request:

```http
  POST /path/to/api/
```
Header request:
| HTTP Header | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `x-api-key` | `string` | **Required**. Provided API key |

Body request is in **JSON** as shown in  `req.json`.

## Response

Response is in **JSON** as shown in  `resp.json`,
it contains a `resp_status` key (the response message status)  
and the possible status codes are `HTTP` compliant as table below :  

| HTTP status code | resp_status                |
| :-------- | :------------------------- |
| `201` | Created ( manifest inserted ) |
| `400` | Bad Request (e.g. missing `awb`) |
| `401` | Unauthorized (e.g. missing `x-api-key` in header) |
| `409` | Conflict ( Manifest already exsists )|
| `500` | server error ( e.g. internal server/db err) |