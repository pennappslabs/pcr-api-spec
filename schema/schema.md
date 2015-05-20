Penn Course Review API
=================

This is the API used by the website and SDK clients.

## Courses

Course resource, e.g. 'CIS-120 in 2011c'. Note that a course may have multiple aliases through crosslistings.

### Attributes

| Name | Type | Description | Example |
| ------- | ------- | ------- | ------- |
| **aliases** | *array* | list of associated aliases | `["PHIL-006"]` |
| **coursehistories:path** | *string* | relative path for a course's history | `"/coursehistories/1428"` |
| **credits** | *number* | number of academic credits associated with course | `1.0` |
| **description** | *string* | course description | `"An introduction to first-order logic including the completeness, compactness, and Lowenheim-Skolem theorems, and Godel's incompleteness theorems."` |
| **id** | *integer* | unique identifier of course | `2041` |
| **name** | *string* | full course title | `"FORMAL LOGIC II"` |
| **path** | *string* | relative path for a course | `"/courses/2041"` |
| **primary_alias** | *string* | unique identifier for course department and number | `"PHIL-006"` |
| **reviews:path** | *string* | relative path for a course's reviews | `"/courses/2041/reviews"` |
| **sections:path** | *string* | relative path to course's sections | `"/courses/2041/sections"` |
| **sections:values** | *array* | array of sections | `[{"aliases"=>["MATH-570-401"], "id"=>"2041-401", "name"=>"FORMAL LOGIC II", "path"=>"/courses/2041/sections/401", "primary_alias"=>"PHIL-006-401", "sectionnum"=>"401"}]` |
| **semester** | *string* | unique identifier for semester | `"2002A"` |

### Courses Info

Info for existing course. You can access this through the course's id (ex: 2041) or using a hyphen separated combination of semester and course identity (ex: 2003A-PHIL-006).

```
GET /courses/{course_id_or_url}
```


#### Curl Example

```bash
$ curl -n http://api.penncoursereview.com/v1/courses/$COURSE_ID_OR_URL
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
        "aliases": [
          "PHIL-006"
        ],
        "coursehistories": {
          "path": "/coursehistories/1428"
        },
        "credits": 1.0,
        "description": "An introduction to first-order logic including the completeness, compactness, and Lowenheim-Skolem theorems, and Godel's incompleteness theorems.",
        "id": 2041,
        "name": "FORMAL LOGIC II",
        "path": "/courses/2041",
        "primary_alias": "PHIL-006",
        "reviews": {
          "path": "/courses/2041/reviews"
        },
        "sections": {
          "path": "/courses/2041/sections",
          "values": [
            {
              "aliases": [
                "MATH-570-401"
              ],
              "id": "2041-401",
              "name": "FORMAL LOGIC II",
              "path": "/courses/2041/sections/401",
              "primary_alias": "PHIL-006-401",
              "sectionnum": "401"
            }
          ]
        },
        "semester": "2002A"
      }
    ]
  },
  "retrieved": "2015-05-19 21:34:22.150788",
  "valid": true,
  "version": "0.3"
}
```


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


## Sections

Course section

### Attributes

| Name | Type | Description | Example |
| ------- | ------- | ------- | ------- |
| **aliases** | *array* | list of associated aliases for a section | `["MATH-570-401"]` |
| **courses:aliases** | *array* | list of associated aliases | `["PHIL-006"]` |
| **courses:id** | *integer* | unique identifier of course | `2041` |
| **courses:name** | *string* | full course title | `"FORMAL LOGIC II"` |
| **courses:path** | *string* | relative path for a course | `"/courses/2041"` |
| **courses:primary_alias** | *string* | unique identifier for course department and number | `"PHIL-006"` |
| **courses:semester** | *string* | unique identifier for semester | `"2002A"` |
| **id** | *string* | unique identifier for section | `"2041-401"` |
| **instructors** | *array* | list of associated instructors | `[{"first_name"=>"JACK", "id"=>"1-JACK-TOPIOL", "last_name"=>"TOPIOL", "name"=>"JACK TOPIOL", "path"=>"/instructors/1-JACK-TOPIOL"}]` |
| **meetingtimes** | *array* | list of section meeting times | `[{"day"=>"W", "start"=>"13:30", "end"=>"15:00", "type"=>"LEC", "room"=>{"id"=>"LEVH 101", "name"=>"Wu and Chen Auditorium", "number"=>"101", "building"=>{"id"=>"LEVH", "latitude"=>13.371337, "longitude"=>90.01, "name"=>"Levine Hall", "path"=>"/building/LEVH"}}}]` |
| **name** | *string* | Course section's full title | `"FORMAL LOGIC II"` |
| **path** | *string* | relative path to course section | `"/courses/2041/sections/401"` |
| **primary_alias** | *string* | unique identifier for section | `"PHIL-006-401"` |
| **sectionnum** | *string* | number for section | `"401"` |

### Sections Info

Info for existing section.

```
GET /sections/{section_id}
```


#### Curl Example

```bash
$ curl -n http://api.penncoursereview.com/v1/sections/$SECTION_ID
```


#### Response Example

```
HTTP/1.1 200 OK
```

```json
{
  "result": {
    "aliases": [
      "MATH-570-401"
    ],
    "courses": {
      "aliases": [
        "PHIL-006"
      ],
      "id": 2041,
      "name": "FORMAL LOGIC II",
      "path": "/courses/2041",
      "primary_alias": "PHIL-006",
      "semester": "2002A"
    },
    "id": "2041-401",
    "instructors": [
      {
        "first_name": "JACK",
        "id": "1-JACK-TOPIOL",
        "last_name": "TOPIOL",
        "name": "JACK TOPIOL",
        "path": "/instructors/1-JACK-TOPIOL"
      }
    ],
    "meetingtimes": [
      {
        "day": "W",
        "start": "13:30",
        "end": "15:00",
        "type": "LEC",
        "room": {
          "id": "LEVH 101",
          "name": "Wu and Chen Auditorium",
          "number": "101",
          "building": {
            "id": "LEVH",
            "latitude": 13.371337,
            "longitude": 90.01,
            "name": "Levine Hall",
            "path": "/building/LEVH"
          }
        }
      }
    ],
    "name": "FORMAL LOGIC II",
    "path": "/courses/2041/sections/401",
    "primary_alias": "PHIL-006-401",
    "sectionnum": "401"
  },
  "retrieved": "2015-05-19 21:34:22.150788",
  "valid": true,
  "version": "0.3"
}
```

### Sections List

List existing sections.

```
GET /sections
```


#### Curl Example

```bash
$ curl -n http://api.penncoursereview.com/v1/sections
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
        "aliases": [
          "MATH-570-401"
        ],
        "courses": {
          "aliases": [
            "PHIL-006"
          ],
          "id": 2041,
          "name": "FORMAL LOGIC II",
          "path": "/courses/2041",
          "primary_alias": "PHIL-006",
          "semester": "2002A"
        },
        "id": "2041-401",
        "instructors": [
          {
            "first_name": "JACK",
            "id": "1-JACK-TOPIOL",
            "last_name": "TOPIOL",
            "name": "JACK TOPIOL",
            "path": "/instructors/1-JACK-TOPIOL"
          }
        ],
        "meetingtimes": [
          {
            "day": "W",
            "start": "13:30",
            "end": "15:00",
            "type": "LEC",
            "room": {
              "id": "LEVH 101",
              "name": "Wu and Chen Auditorium",
              "number": "101",
              "building": {
                "id": "LEVH",
                "latitude": 13.371337,
                "longitude": 90.01,
                "name": "Levine Hall",
                "path": "/building/LEVH"
              }
            }
          }
        ],
        "name": "FORMAL LOGIC II",
        "path": "/courses/2041/sections/401",
        "primary_alias": "PHIL-006-401",
        "sectionnum": "401"
      }
    ]
  },
  "retrieved": "2015-05-19 21:34:22.150788",
  "valid": true,
  "version": "0.3"
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


