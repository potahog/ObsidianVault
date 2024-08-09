---
cssclasses:
  - dashboard
---


## 독서
- 📗현재 읽고 있는 책
	- [[50. Books/51. List of Books/Untitled|Untitled]]
- 📕앞으로 읽을 책
	- [[부의 해답 삶을 지배하고 돈과 성공을 얻어라]]
- 📘독서 노트
	- [[17. 옵시디언 MOC, 대시보드 홈페이지 만들기, 인덱스 노트]]

## 학습
- 🖥코딩 공부
	- [[자바스크립트 기초]]
	- [[파이썬 기초]]
- 💜옵시디언
	- [[DateView 플러그인]]
	- [[Templater 플러그인]]

## 유튜브
- :LiStickyNote:기획
	- [[01_플러그인 활용]]
	- [[02_Css 적용하기]]
	- [[03_옵시디언 꾸미기]]
- 🎥촬영
- 🖥편집

## 노트 리스트
- 🗃 최근 수정한 노트
`$=dv.list(dv.pages('').sort(f=>f.file.mtime.ts,"desc").limit(5).file.link)`
- 📝 최근 작성한 노트
`$=dv.list(dv.pages('').sort(f=>f.file.ctime.ts,"desc").limit(5).file.link)`
- 📁 폴더: 리뷰
  `$=dv.list(dv.pages('"리뷰"').sort(f=>f.file.ctime.ts,"desc").limit(5).file.link)`
- 📑 태그: 자기계발
  `$=dv.list(dv.pages('#자기계발').sort(f=>f.file.name,"desc").limit(5).file.link)`
- ✅ 완료: 프로젝트
  `$=dv.list(dv.pages('').where(p => p.completed === true).sort(f=>f.file.name,"asc").limit(5).file.link)`