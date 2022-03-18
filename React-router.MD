# React Router

## ① SPA (Single Page Application)

* 기존 웹 페이지
: 화면 일부를 다른 이용으로 변환하는 작업 힘들었음. 각 화면에 해당하는 웹 문서 일일이 제작. 서버에 저장된 값 화면에 반영할 수 있는 동적인 웹 문서 생성 도구 개발.



* `index.html` 과 `home.js` 가 있다고 가정할 때,
`index.html` 이라는 빈 종이, `home.js` 는 도장.


* 개발자 도구로 해당 사이트 HTML 소스 확인해보면, `index.html`에 입력된 내용만 보임.



* `index.html` 위에 여러 화면들을 JS 로 구성.
리액트의 경우, `주소(pathname)`에 맞는 컴포넌트 출력.


* index.html
``` javascript
function App ({pathname}) {
 return (
 <div id = "body">
  {pathname === "home" (<Home />)}
  {pathname === "signup" (<Signup />)}
  {pathname === "login" (<Login />)}
 )
}
```


* Home.jsx
```javascript
class Home extends React
...
```


* Signup.jsx
```javascript
class Signup extends React
...
```

* Login.jsx
```javascript
class Login extends React
...
```

* 장단점

  * 장점 : 서버에서 완전히 새로운 페이지 불러오기x 페이지 갱신에 필요한 데이터만 받기o
  = 페이지 전환 속도 빠름. 사용자와 interaction 빠름 등.

  * 단점 : 맨 처음에 페이지 불러올 때, 로딩 시간이 길어진다.
  
  * **코드 스플리팅(code splitting)** 을 사용하면 라우트별로 파일들을 나누어서 트래픽과 로딩 속도 개선 가능
  * 로딩되어 실행될 때, 흰 페이지가 나타날 수 있다는 **서버 사이드 렌더링(server-side rendering)** 사용해서 해결 가능.

-----------------------------------------------
## ② 리액트 라우터 구성

5종류 라우터 있음. 우리는 웹개발로 갈거니 BrowserRouter 사용.

### 1. 설치
	```
	yarn add react-router-dom
	```
### 2. 적용방법
`src/index.js` 파일에서 `react-router-dom`에 내장되어 있는 **BrowserRouter** 라는 컴포넌트 사용해 감싸면 됨.
웹 APP에 HTML5 의 History 를 사용하여 페이지 새로고침 하지 않아도, 주소 변경/현 주소 관련 정보(match, location, history) 조회 및 사용 가능.

### 3. 
