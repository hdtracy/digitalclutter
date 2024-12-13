---
url: https://www.youtube.com/watch?v=JTObSymEvWA
draft: false
tags:
  - obsidian
  - dataview
up: "[[Dataview]]"
---
**Source:** video from Youtube creator, [[Nicole van der Hoeven]] 

- Build a bottom-up approach to note taking and learning
- Think of a DataView query as a superpowered search of your entire vault 

>[!info] Obsidian DataView documentation:
> https://blacksmithgu.github.io/obsidian-dataview/
> https://blacksmithgu.github.io/obsidian-dataview/query/queries/ 


- A dataview query always begins and ends with three backticks, creating what's called a **code block**
	- Next, select the type of view. Supported options are: 
		- LIST
		- TABLE
			- To control column header names of Tables, use the **AS** operator. For example: 
			  ```TABLE location as "Country"```
		- TASK
			- To view only uncompleted tasks (add FROM after TASK to specify source):
			- ```TASK 
			   WHERE !completed```
		- CALENDAR
- DataView query language is also referred to as **DQL** 
- In the first line of the query, specify the **type** of view and optionally, scope to a particular  location or tag using **FROM** 
- Use the **WHERE** keyword to narrow down your results 
	- - Can use **AND** and **OR** operators in the WHERE statements to further narrow down results
- Optionally, you can add the **SORT** option to specify the order in which results are displayed

```
```dataview 
TABLE keywords FROM "Planners"
WHERE type = "video"
SORT file.name ASC
```

```
```dataview 
LIST location
WHERE type = "person" and project = "Project X"
```

>[!tip]- Add a summary field to meeting notes to quickly mention any decisions or action items to be able to pull them all together later
![[Screen Shot 2022-04-13 at 5.23.45 PM.png]]

![[Screen Shot 2022-04-13 at 5.53.02 PM.png]]

![[Pasted image 20220420124244.png]]

###### **Code to embed cover image from URL:** 
```
![Cover](undefined)

*or*

![Cover](https://books.google.com/books/content?id=5u625w2rca8C&printsec=frontcover&img=1&zoom=1&edge=curl&source=gbs_api)
```


![[32435E22-9DFC-47CB-ADF2-690375E7DFD6.jpeg]]


---
source info below from [joschuasgarden.com](https://joschuasgarden.com/50+Slipbox/Dataview+Plugin)

### General
-   The links introduced through dataview are not Obsidian notes, so don't show up in backlinks or the graph
-   Emojis are valid YAML metadata!
-   See note as dataview does: `app.plugins.plugins.dataview.api.page('Note Name')`

### Methods:
-   `file.size`
-   `file.name`
-   `file.mtime`: modified time
-   `file.ctime`: created time
-   `file.tags`: tags of file
-   `file.path`: "Folder/Name.md"

### Lists
-   From tag: `from #moc`
-   From folder: `from "Attachments"`
-   Links
    -   coming into: `from [[Test MOC]]`
    -   going out: `from outgoing([[test moc]])`
-   Logical operators:
    -   `and`
    -   `or`
    -   negate: `list from -#personal`
-   String Concatenation:
    -   `list "File path: " + file.path + " :)"`

### Tasks:
-   Take all check boxes: `task from #moc`

### where {condition}
-   comparison operators:
    -   `<`, `>`, `!=`
-   Examples:
    -   exclude Templates: `WHERE !contains(file.name,"emplate")`
    -   exclude note: `where file.name != "To exclude"
    -   modified at least yesterday: `where file.mtime >= date(today) - dur(1 day)`
    -   without a (or empty) yaml frontmatter field: `where !dueDate`

### Tables
-   `table authors from "Sources"`
-   Sort: `sort file.name asc`
    -   for ties: multiple properties
-   `flatten`: Each author gets own row (duplicate)
-   Grouping:
    -   `table intensity, rows.file.name`
    -   `from "Assignments"`
    -   `group by something`

### Snippets

#### DataviewJS
##### List
```
dv.list(
        dv.pages("").where(p => p.file.folder == "A - Test"
    ).file.link
	)
```

#### Table: Tiers + Owned Checkbox
```javascript
dv.table(["", "Pic", "Title", "Author", "Tier"], dv.pages("#book")
    .where(b => (b.status == "to-read"))
    .sort(b => b.added, "asc")
    .map(b => [readNext(b), `![p|70](${b.urls["thumbnail-url"]})`, b.file.link, b.Author, checkTier(b)])
)

function readNext(book) {
    if (book["read-next"]) {
        console.log(encodeURI(book["read-next"]))
        return `[✅](obsidian://advanced-uri?vault=Vault&filepath=${encodeURI(book.file.name)}.md&search=read-next%253A%2520true&replace=read-next%253A%2520false)`;
    } else {
        return `[⏸](obsidian://advanced-uri?vault=Vault&filepath=${encodeURI(book.file.name)}.md&search=read-next%253A%2520false&replace=read-next%253A%2520true)`;
    }
}

function checkTier(b) {
    if (dv.page(b.Author).poc == "🤎" && dv.page(b.Author).nationality != "🇺🇸" && dv.page(b.Author).gender == "🚺") {
        return "⭐"
    } else if (dv.page(b.Author).poc == "🤎" && dv.page(b.Author).nationality == "🇺🇸" && dv.page(b.Author).gender == "🚺") {
        return "🚺🤎"
    } else if (dv.page(b.Author).poc == "🤎" && dv.page(b.Author).nationality != "🇺🇸" && dv.page(b.Author).gender != "🚺") {
        return "🌐🤎"
    } else if (dv.page(b.Author).poc != "🤎" && dv.page(b.Author).nationality != "🇺🇸" && dv.page(b.Author).gender == "🚺") {
        return "🌐🚺"
    } else if (dv.page(b.Author).poc != "🤎" && dv.page(b.Author).nationality == "🇺🇸" && dv.page(b.Author).gender == "🚺") {
        return "🚺"
    } else if (dv.page(b.Author).poc == "🤎" && dv.page(b.Author).nationality == "🇺🇸" && dv.page(b.Author).gender != "🚺") {
        return "🤎"
    } else if (dv.page(b.Author).poc != "🤎" && dv.page(b.Author).nationality != "🇺🇸" && dv.page(b.Author).gender != "🚺") {
        return "🌐"
    } else {
        return "4: ❌"
    }
}
```

#### Table: Availability
```javascript
dv.table(["Pic", "Title", "Author", "Available?"], dv.pages("#book")
    .where(b => (b.status == "to-read") && (dv.page(b.Author).poc != "🤎" && dv.page(b.Author).nationality == "🇺🇸" && dv.page(b.Author).gender != "🚺"))
    .sort(b => checkAvailability(b), "asc")
    .map(b => [`![p|70](${b.urls["thumbnail-url"]})`, b.file.link, b.Author, checkAvailability(b)])
)

function checkAvailability(b) {
    if (b.owned) {
        return " 🏠 Owned"
    } else if (b.urls["library-url"]?.includes('libby')) {
        return `[📲 Libby](${b.urls["library-url"]})`
    } else if (b.urls["library-url"]?.includes('libris')) {
        return `[🗃 Library](${b.urls["library-url"]})`
    } else if (b.urls["kindle-url"]?.includes('amazon')) {
        return `[🛒 Kindle](${b.urls["kindle-url"]})`
    } else {
        return "*none*"
    }
}
```

#### Sorting
By `tzhou` on [Discord](https://discord.com/channels/686053708261228577/875721010144477204/889082732842479616):
```javascript
.sort(p => p.file.name, 'asc', (a, b) => a.localeCompare(b, 'zh-CN'))
```

#### Pages read percentage
`var pagesRead = dv.current().pagesRead; dv.paragraph("Read: **" + Math.floor((pagesRead / dv.current().pages * 100)) + "**% (" + (dv.current().pages - pagesRead) + "p left)")`

