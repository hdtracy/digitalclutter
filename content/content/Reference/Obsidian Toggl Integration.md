---
{"title":"Obsidian Toggl Integration","draft":false,"tags":["obplugin"],"publish":true,"PassFrontmatter":true,"created":"2024-12-13T15:31:11.151-06:00","updated":"2024-12-13T15:31:58.059-06:00"}
---

[Github](https://github.com/mcndt/obsidian-toggl-integration)  
[Toggl Query Language (TQL) Reference](https://github.com/mcndt/obsidian-toggl-integration/wiki/Toggl-Query-Language-(TQL) 

Let's start with a simply query first. Let's generate an overview of how we spent our time this week. We can do that with the following query:

### Weekly Time Report
```
```toggl
SUMMARY WEEK
```
Which will give you:
```toggl
SUMMARY WEEK
```

---

### Today's Entries
````
```toggl
LIST TODAY 
GROUP BY PROJECT
SORT DESC
```
````
```toggl
LIST TODAY 
GROUP BY PROJECT
SORT DESC
```

---

### Filtering tags

You can filter by tags using the `{INCLUDE|EXCLUDE} TAGS` expression:
-   `INCLUDE TAGS #tag1, #tag2`
-   `EXCLUDE TAGS #tag1, #tag2`

A query may contain both a list of tags to include and to exclude. The resulting report will contain all time entries that have at least one of the tags in the INCLUDE expression, and none of the tags in the EXCLUDE expression.

**Example:**
This query will list all time entries of this month that are tagged as freelance or consulting, AND are not also tagged as billed:
````
```toggl
SUMMARY MONTH
INCLUDE TAGS #freelance, #consulting
EXCLUDE TAGS #billed
```
````

---

### Grouping (only for list reports)

By default, list reports are grouped by date and ordered chronologically. To group by project or client, the `GROUP BY` expression is used:

`GROUP BY {DATE|PROJECT|CLIENT}`

**Example:**
This query will list all time entries in the past two days in the "Reading" or "Obsidian Plugin Development" projects, grouped by project.

````
```toggl
list
past 2 days
include projects "Reading", "Obsidian Plugin Development"
group by project
```
````

This query will result in something like this:
![example-group-by-project](https://user-images.githubusercontent.com/23149353/148293963-39027b50-fbd8-41a2-9b13-9a0dd4723e41.png)

---

### Changing the report appearance

By default, summary reports have a title that reflects the time range of the report query. To change this to a custom title, you can add the following expression at the end of your query:

`TITLE "My title"`

**Example:**
The following query will generate a summary report for the month of January 2022, with the custom title "Fall Semester Finals 2022

````
```toggl
SUMMARY FROM 2022-01-01 TO 2022-01-31
INCLUDE PROJECTS "Examen CG", "Examen QAS"
TITLE "Fall Semester Finals 2022"
```
````

The report's title will look like this:
![custom-title](https://user-images.githubusercontent.com/23149353/148293972-708c6635-a71a-4779-8076-d8a4c9144021.png)

---

### More examples

Here are some more use cases and examples of queries. Feel free to copy and paste these in your own Obsidian client to try for yourself.

**Monthly review**
This query will generate a summary report for December 2021. The list of projects will be ordered in decreasing total spent time.
````
```toggl
SUMMARY FROM 2021-12-01 TO 2021-12-31
SORT DESC
```
````

**Today's entries**
This query will generate a list of time entries logged today, grouped by project and ordered in decreasing total spent time per project.
````
```toggl
LIST TODAY 
GROUP BY PROJECT
SORT DESC
```
````

**Tracking time spent on a school course**
This query will generate a summary report of time spent during the fall semester of 2021 on the "CS 101 Coursework" and "CS 101 Finals Prep" projects in your workspace.
````
```toggl
SUMMARY 
FROM 2021-08-13 TO 2021-12-18
INCLUDE PROJECTS "CS 101 Coursework", "CS 101 Finals Prep"
TITLE "CS 101"
```
````

