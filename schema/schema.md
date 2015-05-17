Penn Course Review API
=================

This is the API used by the website and SDK clients.

## Departments

Academic department at Penn

### Attributes

| Name | Type | Description | Example |
| ------- | ------- | ------- | ------- |
| **id** | *string* | unique 3-4 letter code for department | `"CIS"` |
| **name** | *string* | full name of department | `"COMPUTER AND INFORMATION SCI"` |
| **path** | *string* | relative path for department on the PCR API | `"/depts/cis"` |

### Departments List

List departments.

```
GET /depts
```


#### Curl Example

```bash
$ curl -n http://api.penncoursereview.com/depts
```


#### Response Example

```
HTTP/1.1 200 OK
```

```json
{
  "result": {
    "values": [
      {
        "id": "CIS",
        "name": "COMPUTER AND INFORMATION SCI",
        "path": "/depts/cis"
      }
    ]
  }
}
```


