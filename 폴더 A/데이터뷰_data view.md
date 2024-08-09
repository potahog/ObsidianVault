---
cssclasses:
  - cards
  - cards-1-1
  - cards-corver
---
```dataview
TABLE without id
	("![|100](" + cover_url+ ")") as 표지,
	file.link as 제목,
	tags,
	total_page,
	finishi_read_date,
	book_note
FROM
	"50. Book/51. List of Books"
WHERE
	date(finish_read_date) > date(2023-10-09) OR contains(file.tags, "#자기계발")
SORT
	finish_read_date asc
LIMIT
	10
```