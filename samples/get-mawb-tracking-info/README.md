# API Reference


## Request 
Retrieve tracking information for a MAWB ID.

```http
  GET http://api.glslatina.it/mawb/${mawb-id}
```
This is an example:
```http
  GET https://api.glslatina.it/mawb/123-123456
```

| HTTP Header | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `x-api-key` | `string` | **Required**. Provided API key |

| REST Param | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `mawb-id`      | `string` | **Required**. ID of a valid MAWB e.g. `123-12345678`|


## Response

Response is in **JSON** as shown in  `resp_by_mawb_id.json`,
it contains a `resp_status` key (the response message status)  
and the possible status codes are `HTTP` compliant as table below :  


| HTTP status code | resp_status                |
| :-------- | :------------------------- |
| `200` | ok ( request successfully completed ) |
| `400` | bad params (e.g. missing `mawb-id`) |
| `401` | unauthorized (e.g. missing `x-api-key`) |
| `404` | not found (e.g. invalid `mawb-id`) |
| `500` | server error ( e.g. internal server/db err) |


    

## Request 
Retrieve tracking information for a tracking ID ( GLS parcel ID ).

```http
  GET http://api.glslatina.it/tracking/${tracking-id}
```

This is an example:
```http
  GET http://api.glslatina.it/tracking/LT642428350
```

| HTTP Header | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `x-api-key` | `string` | **Required**. Provided API key |

| REST Param | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `tracking-id`      | `string` | **Required**. ID of a valid tracking ID e.g. `LT641122059`|



## Response

Response is in **JSON** as shown in  `resp_by_tracking_id.json`,
it contains a `resp_status` key (the response message status)  
and the possible status codes are `HTTP` compliant as table below :  

| HTTP status code | resp_status                |
| :-------- | :------------------------- |
| `200` | ok ( request successfully completed ) |
| `400` | bad params (e.g. missing `tracking-id`) |
| `401` | unauthorized (e.g. missing `x-api-key`) |
| `404` | not found (e.g. invalid `tracking-id`) |
| `500` | server error ( e.g. internal server/db err) |

