---
date_monthly: 
tags:
  - "#monthly"
---
```tracker
searchType: frontmatter
searchTarget: exercise
folder: 10. Planner/11. Daily
datasetName: 운동 습관 기르기
month:
	startWeekOn: 'mon'
	headerMonthColor: orange
	initMonth: <% tp.file.title %>
	mode: annotation
	annotation: 💪
```
## 독서 습관
```tracker
searchType: frontmatter
searchTarget: reading_page
folder: 10. Planner/11. Daily
datasetName: 읽은 페이지

line:
	title: 책 읽는 습관
	xAxisLabel: 날짜
	yAxisLabel: 읽은 페이지
	yAxisUnit: 페이지
	lineColor: red
	pointColor: red
	pointBorderWidth: 2
	pointBorderColor: red
	showLegend: True
```
```tracker
searchType: frontmatter
searchTarget: reading_page
datasetName: 읽은 페이지
folder: 10. Planner/11. Daily
startDate: <%* const title = tp.file.title; const firstDay = moment(title + "-01").format('YY-MM-DD dddd'); tR += firstDay; %>
endDate: <%* const year = tp.file.title.split("-")[0]; const month = tp.file.title.split("-")[1]; const lastDay = moment(title).endOf('month').format('YY-MM-DD dddd'); tR += lastDay; %>

summary:
	template: "적게 읽은 날: {{min()::i}}페이지\n많이 읽은 날: {{max()::i}}페이지\n독서한 날: {{numDaysHavingData()::i}}일"
```
