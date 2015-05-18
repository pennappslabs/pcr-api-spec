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
$ curl -n http://api.penncoursereview.com/v1/depts
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


## Instructors

Instructors at Penn

### Attributes

| Name | Type | Description | Example |
| ------- | ------- | ------- | ------- |
| **id** | *string* | unique identifier for instructor | `"1-JACK-TOPIOL"` |
| **first_name** | *string* | first name of instructor | `"JACK"` |
| **last_name** | *string* | last name of instructor | `"TOPIOL"` |
| **name** | *string* | full name of instructor | `"JACK TOPIOL"` |
| **path** | *string* | relative path for instructor on the PCR API | `"/instructors/1-JACK-TOPIOL"` |
| **depts** | *array* | list of associated departments | `["CIS"]` |

### Instructors Info

Info for existing instructor.

```
GET /instructors/{instructor_id}
```


#### Curl Example

```bash
$ curl -n http://api.penncoursereview.com/v1/instructors/$INSTRUCTOR_ID
```


#### Response Example

```
HTTP/1.1 200 OK
```

```json
{
  "id": "1-JACK-TOPIOL",
  "first_name": "JACK",
  "last_name": "TOPIOL",
  "name": "JACK TOPIOL",
  "path": "/instructors/1-JACK-TOPIOL",
  "depts": [
    "CIS"
  ]
}
```

### Instructors List

List existing instructors.

```
GET /instructors
```


#### Curl Example

```bash
$ curl -n http://api.penncoursereview.com/v1/instructors
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
        "id": "1-JACK-TOPIOL",
        "first_name": "JACK",
        "last_name": "TOPIOL",
        "name": "JACK TOPIOL",
        "path": "/instructors/1-JACK-TOPIOL",
        "depts": [
          "CIS"
        ]
      }
    ]
  }
}
```


## Reviews

Course reviews with associated comments

### Attributes

| Name | Type | Description | Example |
| ------- | ------- | ------- | ------- |
| **comments** | *string* | qualitative comments about the course | example |
| **id** | *string* | unique identifier of a review | `"13021-001-297-VAL-BREAZU-TANNEN"` |
| **instructor:first_name** | *string* | first name of instructor | `"JACK"` |
| **instructor:id** | *string* | unique identifier for instructor | `"1-JACK-TOPIOL"` |
| **instructor:last_name** | *string* | last name of instructor | `"TOPIOL"` |
| **instructor:name** | *string* | full name of instructor | `"JACK TOPIOL"` |
| **instructor:path** | *string* | relative path for instructor on the PCR API | `"/instructors/1-JACK-TOPIOL"` |
| **num_reviewers** | *integer* | number of students who chose to review this course offering | `23` |
| **num_students** | *integer* | number of students who took this class and could have reviewed the course | `36` |
| **path** | *string* | relative path for review on the PCR API | `"/courses/13021/sections/001/reviews/297-VAL-BREAZU-TANNEN"` |
| **ratings** | *object* | quantitative ratings given to course |  |
| **section** | *object* | metadata on specific section of course review |  |

### Reviews List

List existing reviews.

```
GET /reviews
```


#### Curl Example

```bash
$ curl -n http://api.penncoursereview.com/v1/reviews
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
        "comments": "example",
        "id": "13021-001-297-VAL-BREAZU-TANNEN",
        "instructor": {
          "first_name": "JACK",
          "id": "1-JACK-TOPIOL",
          "last_name": "TOPIOL",
          "name": "JACK TOPIOL",
          "path": "/instructors/1-JACK-TOPIOL"
        },
        "num_reviewers": 23,
        "num_students": 36,
        "path": "/courses/13021/sections/001/reviews/297-VAL-BREAZU-TANNEN",
        "ratings": null,
        "section": null
      }
    ]
  }
}
```


## Semesters

Academic semester. Spring is A, Summer is B, Fall is C.

### Attributes

| Name | Type | Description | Example |
| ------- | ------- | ------- | ------- |
| **id** | *string* | unique identifier for semester | `"2002A"` |
| **name** | *string* | unique name of semester | `"Spring 2002"` |
| **path** | *string* | relative path for semester on the PCR API | `"/semesters/2002a"` |
| **seasoncode** | *string* | code for semester which maps to Spring, Summer, Fall<br/> **one of:**`"A"` or `"B"` or `"C"` | `"C"` |
| **year** | *integer* | year of semester<br/> **Range:** `2000 <= value <= 2100` | `2002` |

### Semesters Info

Info for existing semester.

```
GET /semesters/{semester_id}
```


#### Curl Example

```bash
$ curl -n http://api.penncoursereview.com/v1/semesters/$SEMESTER_ID
```


#### Response Example

```
HTTP/1.1 200 OK
```

```json
{
  "id": "2002A",
  "name": "Spring 2002",
  "path": "/semesters/2002a",
  "seasoncode": "C",
  "year": 2002
}
```

### Semesters List

List existing semesters.

```
GET /semesters
```


#### Curl Example

```bash
$ curl -n http://api.penncoursereview.com/v1/semesters
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
        "id": "2002A",
        "name": "Spring 2002",
        "path": "/semesters/2002a",
        "seasoncode": "C",
        "year": 2002
      }
    ]
  }
}
```


