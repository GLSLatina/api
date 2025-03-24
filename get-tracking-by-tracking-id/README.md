# API Reference  
## Retrieve tracking information for a tracking (parcel) ID  
  
The following API allows the user to retrieve tracking information for a given GLS tracking-ID ( a.k.a. GLS parcel-ID ).  
Please read all the information contained in this document to successfully complete the integration of this API.

  
## Privacy disclaimer
This document is strictly private, confidential and personal to its recipients and should not be copied, distributed  
or reproduced in whole or in part, nor passed to any third party.

  

## The request  

This is the `endpoint` url to use making a `GET` request :  
```http
  GET http://api.glslatina.it
```
  
with this `path` and the REST `parameter` :  

```http
  /tracking/${tracking-id}
```

  
| REST Param | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `tracking-id`      | `string` | **Required**. The valid GLS ID of a parcel |  

and using this HTTP header :
  
| HTTP Header | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `x-api-key` | `string` | **Required**. Provided API key |


## Sample request  
This is a full working url example:  

```http
  GET http://api.glslatina.it/tracking/LT643635266
```   

A sample call with cURL:  

```http
curl --location --request GET 'https://api.glslatina.it/tracking/LT643635266' \
--header 'x-api-key: YOUR-X-API-KEY'
```  

  
## The response  

The response is in **JSON** format as shown in the `resp_by_tracking_id.json` file in this same directory,

and it has one of these possible status codes are `HTTP` compliant as table below :  
  
| HTTP status code | resp_status                |
| :-------- | :------------------------- |
| `200` | ok ( request successfully completed ) |
| `400` | bad params (e.g. missing `tracking-id`) |
| `401` | unauthorized (e.g. missing `x-api-key`) |
| `404` | not found (e.g. invalid `tracking-id`) |
| `500` | server error ( e.g. internal server/db err) |

  

The JSON content will contain following data:  
| key           | value                                             | type   |
|---------------|---------------------------------------------------|--------|
| `resp_status` | the response message status (ok/errors)           | string |
| `time_zone`   | the timezone of the endpoint                      | string |
| `tracking_id` | the tracking (parcel) ID provided in the request  | string |
| `trackings`   | the list of the tracking events in the GLS system | list   |  
  
  
where each `tracking event` has following data :  

| key                     | value                                                      | type   |
|-------------------------|------------------------------------------------------------|--------|
| `city`                  | the city where the tracking event occurred                 | string |
| `country`               | the country where the tracking event occurred              | string |
| `operating_location`    | the location where the tracking event occurred             | string |
| `operating_time`        | the time where the tracking event occurred                 | string |
| `operation_status_code` | the GLS status code for the tracking event (a.k.a. PDX)    | string |
| `post_code`             | the zipcode (postalcode) where the tracking event occurred | string |
| `state_province`        | the province where the tracking event occurred             | string |
| `tracking_description`  | the description of the tracking event                      | string |  

  