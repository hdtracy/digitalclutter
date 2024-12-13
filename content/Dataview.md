---
url: https://blacksmithgu.github.io/obsidian-dataview/
draft: false
tags:
---
Dataview is a live index and query engine over your personal knowledge base. You can [**add metadata**](https://blacksmithgu.github.io/obsidian-dataview/annotation/add-metadata/) to your notes and **query** them with the [**Dataview Query Language**](https://blacksmithgu.github.io/obsidian-dataview/queries/structure/) to list, filter, sort or group your data. Dataview keeps your queries always up to date and makes data aggregation a breeze.

```dataview
LIST FROM #dataview
```

List from a tag  
<%*  
const dv = app.plugins.plugins["dataview"].api;  
const query = 'list From #dataview';  
let out = await dv.queryMarkdown(query)  
tR += out.value
%>


Serialized:
<!-- QueryToSerialize: LIST FROM #dataview SORT file.name ASC -->
