# 1. Introduction
## 1. Requirements
- ReactJS
	- Nomad Coder Course
		- [ReactJS로 영화 웹 서비스 만들기]()
		- [ReactJS 마스터 클래스]()
- Typescript
- React Hook
- Visual Studio COde
- NodeJS

## 2. What is firebase
Firebase 백엔드 서버 서비스 및 앱 개발 플랫폼으로 웹서비스나 앱을 만들떄 시간을 절약할 수 있음.
만흔 플랫폼을 지원함.
모듈화가 잘 되있어서 많은 기능들 중 사용하고 싶은 기능들만 사용할 수 도 있음.
기본적으로 무료지만 이 프로젝트에서는 유로 수준까지 사용하지 않으며 비용을 절약하는 방법까지 알아볼 것임.
## 3. When Not To Use Firebase
파이어 베이스는 프로토타입에서 용이하고 협업에서는 불편하다고 하지만 파이어페이스는 구글의 서포트를 받을 수 있기때문에 나쁘지 않다.
하지만 앱이 커지면서 커스텀해야하는 경우에는 좋지 않은 선택.

# 2. SetUP

## 1. Installation
Vite, ReactJs 설치
VIte를 이용하여 프로젝트 생성 [vite getting started](https://vitejs.dev/guid)
```
npm create vite@lates
```
위의 명령어를 입력하면 프로젝트명을 입력하고 사용할 프레임워크와 환경변수를 선택할 수 있다.
프레임워크는 React 를 환경 변수는 Typescript + SMC를 선택해서 프로젝트를 만들면 된다.

그러면 터미널에는 아래와 같은 메시지가 출력되며 프로젝트가 생성된다.
```
  cd nwitter-reloaded

  npm install

  npm run dev
```
생성된 프로젝트를 아래 명령어로 vs code를 통해 열어준다.
```
code nwitter-reloaded
```
vs code로 열린 프로젝트에서 terminal을 열어
```
npm install
```
혹은
```
npm i
```
로 프레임워크와 프로젝트 개발환경들을 설치해준다. 프레임워크와 개발환경이 설치가 완료되면 *package.json*을 열어 관련 정보를 확인할 수 있는데 *dev, build, lint, preview 라는 스크립트*가 작성되있는 것을 확인할 수 있다.
```
npm run dev
```
작성된 스크립트는 위의 명령어로 실행할 수 있다.
프로젝트를 시작하기에 앞서 프로젝트를 초기화 시켜줘야 한다. 프로젝트 폴더에서 index.css, app.css, assets폴더를 삭제 해준다. 그리고 App.tsx 파일을 열고 다음과 같이 수정한다.
``` typescript
function App() {

return <></>;

}
export default App;
```
그리고 *main.tsx*파일도 아래와 같이 수정해준다.
``` typescript
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.tsx'

ReactDOM.createRoot(document.getElementById('root')!).render(
<React.StrictMode>
<App />
</React.StrictMode>,
)
```
이렇게 수정하면 npm run dev로 열었던 사이트가 하얗게 초기화 됐을 것이다.

프로젝트 사이트의 제목을 바꿔주기 위해선 *index.html*파일을 열어 다음과 같이 수정해주면 된다.
```html
<!doctype html>
<html lang="en">
<head>
	<meta charset="UTF-8" />
	<meta name="viewport" content="width=device-width, initial-scale=1.0" />
	<title>Nwitter Reloaded</title>
</head>

<body>
	<div id="root"></div>
		<script type="module" src="/src/main.tsx"></script>
	</body>
</html>
```
이 후에는 git을 initialize하고 원격 저장소에 연결을 해주면 된다.
```git
git init .

git remote add origin {원격 git 주소}
```
git 연결이 완료되면 Routing 이나 navigation을 위한 react router dom이나 Style Components와 같은 Dependency들을 설치할 것이다.
Routing과 navigation을 위한 react router dom을 아래의 명령어로 설치하는데 @다음으로 버전을 명시해서 설치한다. (권장하는 버전은 6.14.2)
```
npm install react-router-dom@6.14.2
```
그리고 Style Components를 설치하기 위해서 아래의 명령어를 사용한다.(권장 버전 6.0.7)
```
npm i styled-reset

npm i styled-components@6.0.7

npm i @types/styled-components -D
```



Reference :
[Vite](https://vitejs.dev/guide/)

## 2. Routing
1. App.tsx 에서 새로운 router를 생성
2. router는 createBrowserRouter 함수를 통해 생성
3. 
## 3. LoadingScreen
## 4. Firebase Project


---
#### Tag
#NomadCoder #twitterCloneCouse