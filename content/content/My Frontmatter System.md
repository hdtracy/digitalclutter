---
{"title":"My Frontmatter System","draft":false,"tags":["obsidian"],"publish":true,"PassFrontmatter":true,"created":"2024-12-13T15:12:00.806-06:00","updated":"2024-12-13T15:12:00.806-06:00"}
---

###### Utility Frontmatter
`type`: indicates the type of note. current key pairs used include:
	`type: book`: indicates a book note
	`type: class`: indicates the note is about a specific school class's summary page
	`type: glossary`: to indicate a glossary page or MOC
	`type: lecture_notes`: notes related to school or other educational lectures
	`type: certification`: notes related to a particular professional certification
	`type: plugin`: notes the page is related to an Obsidian plugin
	`type: theme`: notes that the page is about a specific Obsidian theme
	`type: meeting`: indicates a work meeting note
	`type: system`: denotes a page about a utility or organizational "system" within Obsidian

`area`: denotes the note's context
	`area: work`: for work related notes
	`area: school`: for school related notes
	`area: personal`: for personal or unspecified notes


###### Daily Notes Fields for Tracking
`day_rating`: numerical value between 1 and 10 as an overall rating of the day
`sleep_score`: sleep score from sleep tracking app
`sleep_duration`: sleep duration based on sleep tracking app, in format *8h 37m*
`sleep_quality`: quality of sleep assigned by sleep tracker
`stress_score`: day's average stress score according to activity tracker


###### Books
`progress_bar`: used to indicate the current progress through the book (could be used for tasks & projects also)
`cover_img`: used to hold the book cover image for a book note
`total_page`: total page count for the book (*list which book metadata plugin sets this field*)
`rec_source`: source of the recommendation
`goodreads_link`: direct link to book's Goodreads page


###### School
`course_name`: indicates the full name of the course *example: "Programming with Python"*


###### Work
`project_status`: indicates work project status
	`project_status: future`
	`project_status: current`
	`project_status: complete` (may or may not decide to use this one, could be helpful for year-based roll up?)
	`project_status: hibernating`
	`project_status: archived`

`itcr`: indicate ITCR number for project or change (*example: itcr: 38840*)
`meeting_date`: frontmatter to list date of work meeting, in format *YYYY-MM-DD*
`summary`: meeting summary

###### People
`role`: category of person
	`role: content creator`
	`role: manager`
	`role: author`