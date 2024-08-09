```dataview
TABLE without id
	file.link as "책 제목",
	author as "저자",
	("![|50](" + cover_url + ")") as "책 표지",
	tags as "태그", 
	total_page as "페이지", 
	finish_read_date as "읽은 낡짜", 
	book_note as "독서 노트"

FROM "50. Book/51. List of Books"

WHERE
	total_page > 350
```