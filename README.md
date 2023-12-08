# K2WET

## Use Cases


## Authorization


```http
GET /api/HD?call_sign=k2wet
```

| Table | Table Contents | Common Fields
| :--- | :--- | :--- |
| `HD` | Main Form 601 data that carries over to license  | `call_sign` `unique_system_identifier` `license_status` `grant_date` `expired_date` `effective_date` `last_action_date`|
| `EN` | Names and addresses | `call_sign` `unique_system_identifier` `license_status` `grant_date` `expired_date` `effective_date` `last_action_date`|
| `HS` | Application/License History  | `call_sign` `unique_system_identifier` `license_status` `grant_date` `expired_date` `effective_date` `last_action_date`|
| `AM` | Amateur data  | `call_sign` `unique_system_identifier` `license_status` `grant_date` `expired_date` `effective_date` `last_action_date`|
| `CO` | FCC Comments  | `call_sign` `unique_system_identifier` `license_status` `grant_date` `expired_date` `effective_date` `last_action_date`|
| `SC` | License Level Canned Special Conditions  | `call_sign` `unique_system_identifier` `license_status` `grant_date` `expired_date` `effective_date` `last_action_date`|
| `LA` | License Attachment information | `call_sign` `unique_system_identifier` `license_status` `grant_date` `expired_date` `effective_date` `last_action_date`|
| `SF` | License Level Free Form Special Conditions  | `call_sign` `unique_system_identifier` `license_status` `grant_date` `expired_date` `effective_date` `last_action_date`|

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
