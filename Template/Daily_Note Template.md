---
date_daily: <% tp.file.title.slice(0, 8) %>
emotion: 
tags:
  - daily
daily_review: 
important_date: false
achievement: 
reading_book: 
reading_page: 
exercise: false
QT: false
---

<%*
const currentMoment = moment(tp.file.title, "YYYY-MM-DD"); 
tR += '❮ '; 
tR += '[[' + currentMoment.format('YYYY|YYYY년') + ']]' + ' / '; 
tR += '[[' + currentMoment.format('YY-MM|MM월') + ']]' + ' / '; 
tR += '[[' + currentMoment.format('gg-[W]ww') + '|' + currentMoment.format('ww[주]') + ']]'; 
tR += ' ❯'; 
tR += '\n'; 
tR += '❮❮ '; 
currentMoment.add(-1,'days');
tR += '[[' + currentMoment.format('YY-MM-DD dddd|YYYY-MM-DD(ddd)') + ']]' + ' | '; 
currentMoment.add(1,'days'); 
tR += currentMoment.format('YYYY-MM-DD(ddd)') + ' | '; 
currentMoment.add(1,'days'); 
tR += '[[' + currentMoment.format('YY-MM-DD dddd|YYYY-MM-DD(ddd)') + ']]'; 
currentMoment.add(-1,'days'); 
tR += ' ❯❯'; 
%>

<% tp.web.daily_quote() %>

## 내일 기억할 일
-
## 오늘 기억할 일
<%*
	let yesterday = "10. Planner/11. Daily/" + currentMoment.format('YYYY') + "/" + currentMoment.format('MM') + "/" + tp.date.now("YY-MM-DD dddd", -1, tp.file.title, "YY-MM-DD dddd");
	let section = "## 내일 기억할 일";
	let should_include = false;
	let sectionContent = "";

	let yfile = tp.file.find_tfile(yesterday);
	if(yfile) {
		const content = await app.vault.read(yfile);
		if(content.includes(section)) {
			let startIndex = content.indexOf(section) + section.length;
			let endIndex = content.indexOf('\n##', startIndex);
			endIndex = endIndex === -1 ? content.length : endIndex;
			sectionContent = content.substring(startIndex, endIndex).trim();
			should_include = sectionContent.length > 0;
		}
	}

	tR += should_include ? sectionContent : "없습니다😄";
%>

## 아침
### 오늘의 확언
-
### 오늘의 목표
- [ ] 
### 할 일 추가하기
- [ ] 
- [ ] 

## 오늘 끝내야 할 일
```tasks
due on or before <% tp.file.title.slice(0, 8) %>
filter by function task.file.folder.includes("10. Planner")
filter by function !task.file.folder.includes("Template")
not done
sort by priority
```
### 업무 할일
```tasks
tag include #업무
```
### 개인 할일
```tasks
tag include #개인 
```

### 반복 할 일
```tasks
is recurring
not done
has tags
```

### 언젠가 할 일
```tasks
no due date
not done
description regex does not match /^$/
```

### 오늘 완료한 일
```tasks
done <% tp.file.title.slice(0, 8) %>
```

## 독서
- 읽은 책
- 읽은 페이지

## 운동
- 

## 하루 마무리
### 오늘 매운 것들
- 
- 
### 오늘 감사한 일
>[!note]
>
### 일기

## 오늘 작성한 노트
## 오늘 수정한 노트