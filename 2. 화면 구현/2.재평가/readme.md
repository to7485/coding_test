# 📝 메모 애플리케이션 (React)

## 1. 프로젝트 구성

- `create-react-app`으로 프로젝트 생성  
- 필수 의존성 설치:  
  ```bash
  npm install react-router-dom
  ```

---

## 2. 디렉토리 구조

```
/src
 ├ App.js
 ├ index.js
 ├ styles.css
 ├ components/
 │   └ NavBar.js
 ├ pages/
 │   ├ Notes.js
 │   └ AddNote.js
 └ utils/
     └ storage.js
```

---

## 3. 기능 요구사항

### (1) components/NavBar.js

- 상단 고정 메뉴  
- `react-router-dom`의 `Link` 사용  
- 메뉴: `Notes`, `Add Note`  
- 스타일: Light mode 고정  

---

### (2) pages/Notes.js

- `localStorage`에서 메모 목록 불러오기  
- 메모가 없으면 `"No notes yet"` 출력  
- 각 메모 옆에 삭제 버튼 존재  

---

### (3) pages/AddNote.js

- 제목과 내용을 입력받는 form 제공  
- 제출 시 `localStorage`에 메모 추가  
- 추가 후 `/notes`로 이동  

---

### (4) utils/storage.js

- `localStorage` 관련 함수 정의

```js
// 예시 함수 구조
export const getNotes = () => {
  // 로컬스토리지에서 notes 가져오기
};

export const saveNote = (note) => {
  // note 객체 추가
};

export const deleteNote = (id) => {
  // id에 해당하는 메모 삭제
};
```

---

## 4. 디자인 및 스타일 (styles.css)

```css
/* styles.css */

body {
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
}

/* 네비게이션 바 스타일 */
.navbar {
  display: flex;
  gap: 1rem;
  padding: 1rem;
  background-color: #f5f5f5;
  border-bottom: 1px solid #ccc;
}

.navbar a {
  text-decoration: none;
  color: #333;
  font-weight: bold;
}

.navbar a:hover {
  color: #007bff;
}

/* 폼 및 버튼 스타일 */
form {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  padding: 1rem;
}

input, textarea {
  padding: 0.5rem;
  font-size: 1rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 0.5rem;
  background-color: #007bff;
  color: white;
  border: none;
  font-weight: bold;
  cursor: pointer;
  border-radius: 4px;
}

button:hover {
  background-color: #0056b3;
}
```

---

## ✅ 요약

- React 기반의 간단한 메모장
- `react-router-dom`을 활용한 페이지 이동
- `localStorage`를 이용한 데이터 저장 및 삭제
- 기본적인 스타일링 적용 (Light Mode)
