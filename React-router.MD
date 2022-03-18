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

* 5종류 라우터 있음. 우리는 웹개발로 갈거니 BrowserRouter 사용.

* **`라우팅(Routing)`** : 다른 주소에 따라 다른 뷰를 보여주는 과정.
    *"경로에 따라 변경한다"*  라는 의미.

### 1. 설치
	yarn add react-router-dom
### 2. 적용방법
`src/index.js` 파일에서 `react-router-dom`에 내장되어 있는 **BrowserRouter** 라는 컴포넌트 사용해 감싸면 됨.
웹 APP에 HTML5 의 History 를 사용하여 페이지 새로고침 하지 않아도, 주소 변경/현 주소 관련 정보(match, location, history) 조회 및 사용 가능.

### 3. Router 주요 컴포넌트
* **Route**
  ```javascript
  <Route path = "주소규칙" component = {보여 줄 컴포넌트}
  ```
`component`, `render`, `children` 프로퍼티 중 하나 사용해 컴포넌트 출력.
    * **component** : 라우터 공급자로부터 전달받은 모든 값을 프로퍼티로 전달해 출력.
  ```javascript
  <Router path = "/path" component = {MyComponent} />
  ```
   MyComponent 에 `location`, `history`, `match` 프로퍼티가 전달됨.
   <!--
	타입스크립트 사용 시,
	location은
	const location = useLocation();
	params는
	interface MatchProps {
	username: 'velopert' | 'gildong';
	}
	const {username} = useParams();
	-->
  
    * **render** : render 프로퍼티는 render 함수를 구성.
  특정 프로퍼티 사용하고 싶다면
  ```javascript
  <Route path = "/path" render = {props => <MyComponent{...props}/>}
  </Route>
  ```
  와 같이 사용해야함.
  
    조건식 사용할 때,
	```javascript
    <Route path = "*" render = {props => props.match.url === "/someurl" && <MyComponent {...props}/>
    /Route>}
    ```
    일 경우, 주소가 `/someurl` 일 경우에만 MyComponent 출력.
    * **children** : 자식 프로퍼티 형태로 출력.


    * Router 컴포넌트가 출력하는 프로퍼티
    * `match` : 현재 루트에 정의된 경로와 일치한 주소 정보
    * `location` : 브라우저 라우터의 경우 window.location 의 정보 전달.
    * `history` : 페이지 이동 기록 정보. 페이지 앞뒤로 이동할 수도 있음.

* **Switch**
자식으로 배치된 Route 컴포넌트 중 처음으로 조건 만족한 하나의 컴포넌트만 출력해준다.
```javascript
<Switch>
  <Route path = "/login" component = {Login} />
  <Route path = "/" component = {Index} />
</Switch>
```
  해당 코드일 경우, `/login` 이라는 주소가 입력될 때, 첫번째 컴포넌트만 출력.
  만약 Switch 가 없다면, 두 컴포넌트 모두 출력.

* **Link**
경로 변경하는 컴포넌트. 주소와 리액트 라우터 정보면 변경시키기 때문에 **새로고침 현상 방지할 때** 사용.
*ReactDOM 으로 render 시키면 <Link> 컴포넌트는 <a> 태그로 바뀐다.*
```javascript
	<Link to = "주소"> 내용 </Link>
```


* 정리해서 말해보자면,
  * `Switch`, `Route` : 경로 매칭.
  Switch는 감싸진 여러 <Route> 중 경로 일치하는 단 하나만 렌더링.
  Route 는 path 속성 지정하여, 해당 path 에 어떤 컴포넌트 보여줄지 정하는 역할. (<Link> 가 정해주는 URL 경로와 일치하는 경우에만 작동)
  * `Link` : 페이지 새로고침 하지 않고, 경로 변경하는 역할.
  
  
* **Redirect**
특정 조건에서 바로 페이지 이동 해야 하는 경우 사용.
```javascript
{isFinished && <Redirect to = "/home" />}
```



## ③ 파라미터/쿼리
페이지 주소 정의하는 방법은 파라미터/쿼리 사용 가능.
```
파라미터 : /profiles/me
쿼리 : /about?details = true
```
일반적으로,
**파라미터** : 특정 `id`, `이름`으로 조회
**쿼리** : 어떤 `키워드`를 갖고 검색 및 요청


## ④ 서브라우트
탭 처럼 사용 가능.
https://react.vlpt.us/react-router/03-subroutes.html



