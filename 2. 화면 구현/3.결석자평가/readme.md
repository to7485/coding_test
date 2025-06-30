# React 테마 블로그 프로젝트

## 1. 프로젝트 구성

CRA(Create React App)로 프로젝트 생성  
필수 의존성 설치: react-router-dom

---

## 2. 디렉터리 구조

```
/src
 ├ App.js
 ├ context/
 │   └ ThemeContext.js
 ├ index.js
 ├ styles.css
 ├ components/
 │   └ NavBar.js
 └ pages/
     ├ Home.js
     ├ About.js
     └ BlogList.js
```

---

## 3. 요구사항

### (1) ThemeContext 설정 (/src/context/ThemeContext.js)

- createContext를 사용하여 컨텍스트 생성
- ThemeProvider에서 theme(light 또는 dark) 상태와 toggleTheme 함수 제공

---

### (2) App.js

- BrowserRouter로 라우팅 구성
- NavBar 컴포넌트 상단에 배치
- 테마에 따라 배경과 글자색 다르게 적용

```js
const appStyle = {
  backgroundColor: theme === 'light' ? '#ffffff' : '#222222',
  color: theme === 'light' ? '#000000' : '#ffffff',
  minHeight: '100vh',
  padding: '1rem'
};
```

라우팅:

- `/` → Home.js
- `/about` → About.js
- `/blogs` → BlogList.js

---

### (3) NavBar.js

- Link 컴포넌트 사용
- 테마에 따라 navbar-light 또는 navbar-dark 클래스를 조건부 적용
- 스타일은 styles.css에 정의

---

### (4) Home.js

- “Welcome to the Blog!” 메시지 표시
- 현재 테마 표시

---

### (5) About.js

- 간단한 소개 문구 출력

---

### (6) BlogList.js

- useEffect로 JSONPlaceholder API 호출  
  (https://jsonplaceholder.typicode.com/posts?_limit=5)
- 로딩 중에는 “Loading...” 표시
- 에러 발생 시 에러 메시지 표시
- 게시글 제목 리스트 출력

---

## 4. 스타일(styles.css)

```css
.navbar {
  display: flex;
  gap: 1rem;
  padding: 1rem;
  font-weight: bold;
}
.navbar-light {
  background-color: #eee;
}
.navbar-dark {
  background-color: #444;
}
.navbar a {
  text-decoration: none;
  color: inherit;
}
```
