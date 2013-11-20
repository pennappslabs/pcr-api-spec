

# PennCourseReview Search Endpoint

- Author: Ceasar Bautista <ceasarb@seas.upenn.edu>
- Status: Draft
- Created: 24-Sep-2013

# Introduction

The PennCourseReview search endpoint is a service that enable API developers to search for courses, instructors, and departments.

## Scenarios

In designing products, it helps to imagine a few real life stories of how actual (stereotypical) people would use them. We'll look at two scenarios.

### Scenario 1

Consider that we (Labs) make use of search for the autocomplete feature on PennCourseReview.

When a user types in the search box on the PennCourseReview front-end, the server sends a request to `/autocomplete_data.json/(.*)` with the user's query. That route then hits our API and returns a JSON document representing courses, instructors, and departments relevant to the query.

Moving the dataset endpoint to the server has the immediate advantage of reducing the number of requests our server makes and achieves better separation of concerns.

### Scenario 2

Consider a developer who wants to plot course review data for each department on separate graphs, like [CourseGrapher][4].

On such a site it may be desirable to, in addition to enable users to locate a specific course on a graph, enable users to search directly for a course of interest.

## Non-Goals

This version will neither commit to nor describe any relevance metrics for responses. The ordering of results is subject to change at will.

# Overview

Returns a mixed collection of relevant resources (courses, instructors, departments) matching a specified query.

## Resource Information

<table>
    <tbody>
        <tr>
            <td>URL</td>
            <td><code>http://api.penncoursereview.com/1.1/search</code></td>
        </tr>
        <tr>
            <td>HTTP Methods</td>
            <td>GET</td>
        </tr>
        <tr>
            <td>Response Formats</td>
            <td>json</td>
        </tr>
        <tr>
            <td>Rate Limited?</td>
            <td>No</td>
        </tr>
        <tr>
            <td>Authentication</td>
            <td>None</td>
        </tr>
        <tr>
            <td>API Version</td>
            <td>v1.1</td>
        </tr>
    </tbody>
</table>

## Request Information

### Parameters

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Default</th>
            <th>Description</th>
            <th>Example Values</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><tt>q</tt></td>
            <td><strong>Required</strong></td>
            <td>A search query.</td>
            <td><tt>econ</tt>, <tt>spiegel</tt></td>
        </tr>
        <tr>
            <td><tt>result_type</tt></td>
            <td><tt>mixed</tt></td>
            <td>
                <p>The type of results to fetch. Valid values include:</p>
                <br>
                <tt>mixed</tt>: Include courses, instructors, and departments.
                <br>
                <tt>courses</tt>: Include courses.
                <br>
                <tt>instructors</tt>: Include instructors.
                <br>
                <tt>departments</tt>: Include departments.
            </td>
            <td><tt>departments</tt>, <tt>mixed</tt></td>
        </tr>
        <tr>
            <td><tt>count</tt></td>
            <td><tt>15</tt></td>
            <td>The number of results to return per page.</td>
            <td><tt>11</tt>, <tt>7</tt></td>
        </tr>
        <tr>
            <td><tt>page</tt></td>
            <td><tt>0</tt></td>
            <td>The page to fetch.</td>
            <td><tt>2</tt>, <tt>5</tt></td>
        </tr>
    </tbody>
</table>

### Example

GET: `http://api.penncoursereview.com/1.1/search?q=econ&result_type=mixed&count=3`

## Response Information

A response returns multiple datasets.

Note: Responses are compatible with [typeahead.js][1].

### Example

<pre>
{
    "courses": [
        {
            "aliases": [
                "ECON-001"
            ],
            "description": "Discussion of special research topics",
            "name": "INTRO TO MICRO",
            "path": "/courses/ECON-001",
            "semester": "2012C",
            "tokens": [
              "econ001",
              "econ-001",
              "econ",
              "001",
              "intro",
              "to",
              "micro"
            ],
            "value": "ECON 001"
        }, {
            "aliases": [
                "CIS-120"
            ],
            "description": "Introduction to the fundamental concepts of programming.",
            "name": "PROG LANG & TECH I",
            "path": "/courses/CIS-120",
            "semester": "2012C",
            "tokens": [
              "cis120",
              "cis-120",
              "cis",
              "120",
              "prog",
              "lang",
              "&",
              "tech",
              "i"
            ],
            "value": "CIS 120"
        }
    ],
    "instructors": [
        {
            "path": "/instructors/1360-URIEL-SPIEGEL",
            "tokens": [
                "uriel",
                "spiegel",
            ],
            "value": "Uriel Spiegel"
        }, {
            "path": "/instructors/2182-CARITA-C--HUANG",
            "tokens": [
                "carita",
                "c.",
                "huang",
            ],
            "value": "Carita C. Huang"
        }
    ],
    "departments": [
        {
            "id": "ECON",
            "path": "/depts/ECON",
            "tokens": [
                "econ",
                "economics"
            ],
            "value": "Economics"
        }, {
            "id": "CIS",
            "path": "/depts/CIS",
            "tokens": [
                "cis",
                "computer",
                "and",
                "information",
                "science"
            ],
            "value": "Computer and Information Science"
        }
    ]
}
</pre>

### Datum

A datum is an individual unit of a dataset.

The canonical form of a datum has three parts:

- `value`: a string that represents the underlying value of the datum.
- `token`: an array of single-word strings that aids in matching a datum with a given query.
- `path`: a string that represents the path to the full object.

<table>
    <thead>
        <tr>
            <td>Type</td>
            <td>Example</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Course</td>
            <td>
<pre>
{
    "aliases": [
        "ECON-001"
    ],
    "description": "Discussion of special research topics",
    "name": "INTRO TO MICRO",
    "path": "/courses/ECON-001",
    "semester": "2012C",
    "tokens": [
      "econ001",
      "econ-001",
      "econ",
      "001",
      "intro",
      "to",
      "micro"
    ],
    "value": "ECON 001"
}
</pre>
            </td>
        </tr>
        <tr>
            <td>Instructor</td>
            <td>
<pre>
{
    "value": "Uriel Spiegel",
    "tokens": [
        "uriel",
        "spiegel"
    ],
    "path": "/instructors/1360-URIEL-SPIEGEL"
}
</pre>
            </td>
        </tr>
        <tr>
            <td>Department</td>
            <td>
<pre>
{
    "value": "Economics",
    "tokens": [
        "economics"
    ],
    "path": "/depts/ECON",
    "id": "ECON"
}
</pre>
            </td>
        </tr>
    </tbody>
</table>

[1]: http://twitter.github.io/typeahead.js/ "typeahead.js"
[2]: https://github.com/pennappslabs/pcr/blob/master/apps/searchbar/views.py
[3]: https://github.com/pennappslabs/pcr/blob/master/media/front-end/coffee/searchbox.coffee
[4]: http://coursegrapher.appspot.com/
