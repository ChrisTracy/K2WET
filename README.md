# K2WET


## Examples

```http
GET /api/HD?call_sign=k2wet
```
```http
GET /api/EN?first_name=John&L
```

| Table | Table Contents | Common Fields
| :--- | :--- | :--- |
| `HD` | Main Form 601 data that carries over to license  | `call_sign` `unique_system_identifier` `license_status` `grant_date` `expired_date` `effective_date` `last_action_date`|
| `EN` | Names and addresses | `call_sign` `unique_system_identifier` `entity_name` `first_name` `last_name` `street_address` `city` `state` `zip_code`|
| `HS` | Application/License History  | `callsign` `unique_system_identifier` `code` `log_date` |
| `AM` | Amateur data  | `callsign` `unique_system_identifier` `operator_class` `group_code` `region_code` `previous_operator_class`|
| `CO` | FCC Comments  | `call_sign` `unique_system_identifier` `comment_date` `description` |
| `SC` | License Level Canned Special Conditions  | `call_sign` `unique_system_identifier` `special_condition_type` `special_condition_code` |
| `LA` | License Attachment information | `call_sign` `unique_system_identifier` `attachment_code` `attachment_desc` `attachment_date` `action_performed` |
| `SF` | License Level Free Form Special Conditions  | `call_sign` `unique_system_identifier` `lic_freeform_cond_type` `unique_lic_freeform_id` `lic_freeform_condition` |

## Responses
If an valid request is submitted, the api returns a JSON response in the following format:
```javascript
{
  "status_code" : 200
  "message" : ok
  "data" : [json_data]
}
```
If an valid request is submitted, but there is nothing in the database that matches the criteria, the api returns an empty JSON response:
```javascript
{
  "status_code" : 200
  "message" : ok
  "data" : []
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
