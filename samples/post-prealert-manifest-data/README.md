# API Reference

## Request 
The following API allows the sending of manifest pre-alert data to the GLS-LT system.  

URL request:

```http
  POST http://api.glslatina.it/prealert
```

Header request:
| HTTP Header | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `x-api-key` | `string` | **Required**. Provided API key |

Body request is in **JSON** as shown in  `req.json`;  

The structure base of the JSON request is:

```
Common MAWB Information
|_cartons
  |_parcels
    |_items
```

Below you will find the guidelines with the parameters to construct the request JSON. The parameters are essential, mandatory, and for convenience, cast to strings. You will also find examples of the parameters. Additionally, I strongly recommend looking at an example of the request JSON. Please adhere to the format.

**Note**: the `manifest_file_data` json object is still under review.

### Manifest Data - General information

| Params                  | Max Len | Type   | Required | Description                       | Example                      |
|-------------------------|---------|--------|----------|-----------------------------------|------------------------------|
| ecommerce_name          | 255     | string | YES      | Name of the e-commerce            | TEMU                         |
| mawb                    | 31      | string | YES      | Master Air Waybill                | 112-13492135                 |
| flight                  | 31      | string | YES      | Flight number                     | QR8941                       |
| eta                     | 22      | string | YES      | Estimated time of arrival (Format: `mm/dd/yyyy HH:MM:SS AM or PM` )| 12/04/2022 2:00:00 PM|
| etd                     | 22      | string | YES      | Estimated time of departure (Format: `mm/dd/yyyy HH:MM:SS AM or PM` )| 12/03/2022 4:00:00 AM|
| airport_code_departure  | 7       | string | YES      | Airport code of departure         | FCO                          |
| airport_code_destination| 7       | string | YES      | Airport code of destination       | CAN                          |
| total_box_num           | 10      | string | YES      | Total number of boxes             | 104                          |
| total_no_of_packets     | 10      | string | YES      | Total number of packets           | 2843                         |
| pcs_total_weight        | 10      | string | YES      | Total weight of pieces            | 2156                         |
| manifest_data           | -       | object | YES      | List of cartons                   | The example is in the Next table|

### Manifest Data - Cartons

| Params         | Max Len | Type   | Required | Description                       | Example                      |
|----------------|---------|--------|----------|-----------------------------------|------------------------------|
| carton_code    | 31      | string | YES      | Carton identifier                 | 60V2406160623802             |
| parcels        | -       | object | YES      | List of parcels                   | The example is in the next table|


### Manifest Data - Parcels

| Params            | Max Len | Type   | Required | Description                              | Example                    |
|-------------------|---------|--------|----------|------------------------------------------|----------------------------|
| tracking_number   | 31      | string | YES      | Shipment tracking number                 | LT621783955                |
| invoice_number    | 31      | string | YES      | Invoice number                           | BG2211281004925            |
| reference_code    | 31      | string | YES      | Order code                               | WT2233301256001846         |
| shipper_name      | 127     | string | YES      | Name of the shipper                      | TechShop Ltd               |
| ship_add1         | 255     | string | YES      | Shipper address line 1                   | GUANGX HONG MAIN RD NANCUN TOWN PANYU DTRC N6 |
| ship_city         | 127     | string | YES      | Shipper city                             | GUANGZHOU                    |
| ship_state        | 31      | string | YES      | Shipper state                            | CINA                         |
| ship_country_code | 15      | string | NO       | Shipper country code                     | 455444                       |
| consignee_address1| 255     | string | YES      | Consignee address                        | VIA MATTIA BATTISTINI, 15    |
| consignee_city    | 127     | string | YES      | Consignee city                           | Roma                         |
| consignee_zip_code| 15      | string | YES      | Consignee zip code (postal code)         | 00168                        |
| consignee_province| 127     | string | YES      | Consignee province code                  | RM                           |
| consignee_name    | 127     | string | YES      | Consignee name                           | MARIO ROSSI                  |
| consignee_phone   | 63      | string | YES      | Consignee phone number                   | 3402737104                   |
| items             | -       | object | YES      | List of items                            | The example is in the next table|

### Manifest Data - Items

| Params            | Max Len | Type   | Required | Description                              | Example                    |
|-------------------|---------|--------|----------|------------------------------------------|----------------------------|
| item_sku          | 63      | string | YES      | Product SKU code                         | sn2206205570377382         |
| item_hscode       | 15      | string | YES      | Product HS code                          | 950300                     |
| item_description  | 127     | string | YES      | Product description                      | Toy                        |
| total_weight      | 10      | string | YES      | Shipment weight in KG                    | 0.06                       |
| total_value       | 10      | string | YES      | Total purchase amount in EUR             | 2.55                       |
| vat_value         | 10      | string | YES      | VAT amount                               | 0.56                       |
| ioss_number       | 15      | string | YES      | Import One Stop Shop number              | IM3720013929               |


## Response

Response is in **JSON** as shown in  `resp.json`. It contains a `resp_status` key (the response message status):

| Name            | Type   | Description                        |
|-----------------|--------|------------------------------------|
| resp_status     | string | Response status: "ok" or "err" with log    |
| time_zone       | string | Time zone of the response          |
| operating_time  | string | Time of operation `(YYYY-MM-DD HH:MM:SS)` |

and the possible status codes are `HTTP` compliant as table below :  

| HTTP status code | resp_status                |
| :-------- | :------------------------- |
| `201` | Created ( manifest inserted ) |
| `400` | Bad Request (e.g. missing `awb`) |
| `401` | Unauthorized (e.g. missing `x-api-key` in header) |
| `409` | Conflict ( Manifest already exsists )|
| `500` | server error ( e.g. internal server/db err) |
