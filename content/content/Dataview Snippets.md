---
{"title":"Dataview Snippets","draft":false,"tags":["dataview","obsidian"],"publish":true,"PassFrontmatter":true,"created":"2024-12-13T14:51:34.390-06:00","updated":"2024-12-13T14:51:34.390-06:00"}
---

# Dataview Snippets

>[!note] Note:
>These code blocks are set as sql syntax in order to better display the code that should be used in the dataview queries.

### **Day Tracker Stats Table**
```sql
table without id
file.link AS "Day",
sleep_score AS "Sleep Score",
sleep_quality AS "Sleep Quality",
sleep_duration AS "Sleep Duration",
stress_score AS "Stress Score"
FROM #daily_note AND "Planners"
WHERE (file.mtime >= (date("<% tp.date.weekday("YYYY-MM-DD",0) %>"))) and (file.ctime <= date("<% tp.date.weekday("YYYY-MM-DD",6) %>")+dur(1 day)) 
SORT file.day 
```

### **Memories Table**
```sql
table
memories AS "Entry"
FROM #daily_note 
WHERE memories and (file.mtime >= (date("2022-04-24"))) and (file.ctime <= date("2022-04-30")+dur(1 day)) 
SORT file.day 
```


### **Daily Note links to Weekly Summary and next/previous day**
```sql
<< [[<% moment(tp.file.title,'YYYY-MM-DD').add(-1,'days').format("YYYY-MM-DD") %>]] | [[Weekly Review <% tp.date.weekday("YYYY-[W]ww (MMM-DD)",0, tp.file.title, "YYYY-MM-DD") %>]]  | [[<% moment(tp.file.title,'YYYY-MM-DD').add(1,'days').format("YYYY-MM-DD") %>]] >>
```


### **Weekly Summary rollup of day_summary from daily notes**
```sql
table
day_summary AS "Some Lines a Day",
day_rating AS "Day Rating"
FROM "Planners" AND #daily_note 
WHERE day_summary AND (file.mtime >= (date("<% tp.date.weekday("YYYY-MM-DD",0) %>"))) and (file.ctime <= date("<% tp.date.weekday("YYYY-MM-DD",6) %>")+dur(1 day)) 
SORT file.day 
```


### **Table of Podcast log entries from daily notes** based on [[Leah Ferguson\|Leah Ferguson]]'s [[Start and End your Day with a Daily Note\|Start and End your Day with a Daily Note]]
```sql
TABLE
log-podcast AS Podcast
FROM "00 - Meta/06 - Planners/Dailies"
WHERE log-podcast
FLATTEN date
SORT date desc
```


### **Table of D&D session log entries from notes** based on [[Leah Ferguson\|Leah Ferguson]]'s 
```sql
TABLE WITHOUT ID 
	link(file.link,aliases) as "Session", 
	date-session as "IRL Date", 
	campaign-date as "Date", 
	tldr 
FROM "60 Games/62 Campaigns/62.04 Hoard of the Dragon Queen/02 Sessions" 
WHERE contains(type, "session") 
WHERE !contains(title, "S00") 
SORT date-session asc
```


### **Dataview snippet for People note**
```sql
TABLE 
    WITHOUT ID
    link(Source, dateformat(date(Source), "yyyy-MM-dd")) as "", 
    rows.Details as "Details"
FROM "00 Meta/02 Journal/02.01 Daily"
WHERE  contains(log, this.file.name)
FLATTEN log as Details
WHERE contains(Details, this.file.name)
GROUP BY file.link as Source
SORT rows.file.day desc
```


### **Style Dataview Table Columns**
**Basic**
```
TABLE 
	publisher,
	developer,
    "<span style='display:flex; justify-content: right;'>" + price + "</span>" AS Price
FROM "10 Example Data/games"
```

> [!info] Other style possibilities For bold, italic, highlighted or strikethrough text, see the first variant. **Underscore text**: `<span style='text-decoration: underline;'>` **Right alignment**: `<span style='display:flex; justify-content: right;'>` **Center alignment**: `<span style='display:flex; justify-content: center;'>` **Make text uppercase**: `<span style='text-transform: uppercase;'>` **Text color**: `<span style='color: red;'>`

**Use bold, italic or highlight text styles**
> [!info] Available styles You can use every style [Obsidian has available](https://help.obsidian.md/How+to/Format+your+notes) this way.
```
TABLE 
	"_" + publisher + "_" AS Publisher,
	"**" + developer + "**" AS Developer,
    "==" + price + "==" AS Price
FROM "10 Example Data/games"
```

**Style multiple columns**
```
TABLE styleStart + author + styleEnd AS Author, 
	genres, 
	styleStart + totalPages + styleEnd AS "Total Pages"
FROM "10 Example Data/books"
FLATTEN "<span style='display:flex; justify-content: center;'>" AS styleStart
FLATTEN "</span>" AS styleEnd
```

**Use different styles**
```
TABLE greenStyle + author + styleEnd AS Author, 
	genres, 
	rightAlignStyle + totalPages + styleEnd AS "Total Pages"
FROM "10 Example Data/books"
FLATTEN "<span style='color: lightgreen;'>" AS greenStyle
FLATTEN "<span style='display:flex; justify-content: right;'>" AS rightAlignStyle
FLATTEN "</span>" AS styleEnd
```

**Style page link**
```
TABLE WITHOUT ID styleStart + file.link + styleEnd AS "Book", 
	author,
	totalPages
FROM "10 Example Data/books"
FLATTEN "<span style='text-transform: uppercase;'>" AS styleStart
FLATTEN "</span>" AS styleEnd
```

### Calendar
```sql
CALENDAR file.day
FROM "10 Example Data/dailys" OR #journal
```


### Dataview for Tasks due today or earlier
```sql
TASK 
WHERE !completed AND duedate AND duedate <= date(today) AND contains(text, "due")
```


### Show tasks with a due date
```sql
TASK
FROM "10 Example Data/assignments"
WHERE duedate
```