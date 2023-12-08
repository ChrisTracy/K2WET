# K2WET ULS API

## About the Project

This api is built on top of [sqliteRest](https://github.com/ChrisTracy/sqliteRest). Data is is served exactly as it sits in the sqlite database. The table name is defined in the route and queries follow a question mark. The ULS database is rebuilt and refreshed every monday morning (4AM - 6AM CST) using [ULS2sqlite](https://github.com/ChrisTracy/sqliteRest).
```http
GET /api/{table_name}?field1=value&field2=value2
```

## Examples

Get 601 form data for specified call sign 
```http
GET /api/HD?call_sign=k2wet
```
Get name and address information for anyone with the last name Smith in Richmond VA
```http
GET /api/EN?city=richmond&state=va&last_name=smith
```
A wildcard lookup for anyone with the last name Johnson and a first name containing the letter "j" in Los Angeles CA
```http
GET /api/EN?city=los angeles&state=ca&last_name=johnson&first_name=j*
```
The API will only return the fields if there is a value in it. If you want all of the fields you can use the all_fields parameter
```http
GET /api/HD?call_sign=k2wet&all_fields=true
```

## Endpoints and parameters

| Table | Table Contents | Common Fields
| :--- | :--- | :--- |
| `HD` | Main Form 601 data that carries over to license  | `call_sign` `unique_system_identifier` `license_status` `grant_date` `expired_date` `effective_date` `last_action_date`|
| `EN` | Names and addresses | `call_sign` `unique_system_identifier` `entity_name` `first_name` `last_name` `street_address` `city` `state` `zip_code`|
| `HS` | Application/License History  | `callsign` `unique_system_identifier` `code` `log_date` |
| `AM` | Amateur data  | `callsign` `unique_system_identifier` `operator_class` `group_code` `region_code` `previous_operator_class`|
| `CO` | FCC Comments  | `callsign` `unique_system_identifier` `comment_date` `description` |
| `SC` | License Level Canned Special Conditions  | `callsign` `unique_system_identifier` `special_condition_type` `special_condition_code` |
| `LA` | License Attachment information | `callsign` `unique_system_identifier` `attachment_code` `attachment_desc` `attachment_date` `action_performed` |
| `SF` | License Level Free Form Special Conditions  | `callsign` `unique_system_identifier` `lic_freeform_cond_type` `unique_lic_freeform_id` `lic_freeform_condition` |

## Responses
If a valid request is submitted, the api returns a JSON response in the following format:
```javascript
{
  "status_code" : 200
  "message" : ok
  "data" : [json_data]
}
```
If a valid request is submitted, but there is nothing in the database that matches the criteria, the api returns an empty JSON response:
```javascript
{
  "status_code" : 404
  "message" : "No data found for table {table_name} with conditions {params}"
}
```

If an invalid request is submitted, or some other error occurs, the api returns a JSON response in the following format:

```javascript
{
  "status_code" : 400, 404, or 500
  "message" : string
}
```

## Status Codes

Gophish returns the following status codes in its API:

| Status Code | Description |
| :--- | :--- |
| 200 | `OK` |
| 400 | `BAD REQUEST` |
| 404 | `NOT FOUND` |
| 500 | `INTERNAL SERVER ERROR` |

##Rate Limits
As of right now the api supports 500 records returned and 8 requests per 10 seconds. These limits are subject to change. If you need higher limits you can easily deploy this app with the two libraries listed above. 

## Notes

As stated above, data is served through the api exactly as it sits on the FCC ULS database. Why they used "call_sign" in the first two tables and "callsign" in the other six tables is a mystery to me. 
