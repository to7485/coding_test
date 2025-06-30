## 정답
### login.html
```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>로그인</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="login.css">
  <script src="login.js" defer></script>
</head>
<body>
  <div class="login-container">
    <form id="loginForm">
      <h2>로그인</h2>
      <label for="username">아이디</label>
      <input type="text" id="username" placeholder="아이디를 입력하세요">
      <small id="usernameMsg"></small>
      <label for="password">비밀번호</label>
      <input type="password" id="password" placeholder="비밀번호를 입력하세요">
      <button type="submit">로그인</button>
    </form>
  </div>
</body>
</html>
```

### login.css
```css
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR&display=swap');
body {
  font-family: 'Noto Sans KR', sans-serif;
  background-color: #f2f2f2;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}.login-container {
  width: 100%;
  max-width: 350px;
  padding: 2rem;
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}input {
  padding: 0.6rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 1rem;
}button {
  padding: 0.6rem;
  background-color: #3498db;
  color: #fff;
  font-size: 1rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}button:hover {
  background-color: #2980b9;
}small {
  color: red;
  font-size: 0.8rem;
}@media (max-width: 600px) {
  .login-container {
    margin: 1rem;
    width: 90%;
  }
}
```

### login.js
```js
document.getElementById("loginForm").addEventListener("submit", function(e) {
  e.preventDefault();
  alert("로그인되었습니다");
  window.location.href = "board.html";
});

document.getElementById("username").addEventListener("input", function() {
  document.getElementById("usernameMsg").textContent = "아이디 입력 중...";
});
```


### board.html
```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>게시판</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: 'Noto Sans KR', sans-serif;
      background-color: #f8f8f8;
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
    }
    .board-container {
      width: 90%;
      max-width: 800px;
      background-color: #fff;
      padding: 2rem;
      border-radius: 8px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }
    h2 {
      text-align: center;
    }
    .btn-group {
      display: flex;
      justify-content: flex-end;
      gap: 0.5rem;
      margin-bottom: 1rem;
    }
    button {
      padding: 0.5rem 1rem;
      background-color: #3498db;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      transition: background-color 0.3s;
    }
    button:hover {
      background-color: #2980b9;
    }
    table {
      width: 100%;
      border-collapse: collapse;
    }
    th, td {
      padding: 0.75rem;
      border: 1px solid #ccc;
      text-align: center;
    }
    tr:hover {
      background-color: #f0f8ff;
    }
  </style>
</head>
<body>
  <div class="board-container">
    <h2>게시판</h2>
    <div class="btn-group">
      <button onclick="location.href='login.html'">로그아웃</button>
      <button onclick="location.href='personal_info.html'">개인정보수정</button>
    </div>
    <table>
      <thead>
        <tr><th>제목</th><th>작성자</th></tr>
      </thead>
      <tbody>
        <tr><td>안녕하세요</td><td>관리자</td></tr>
        <tr><td>공지사항</td><td>관리자</td></tr>
      </tbody>
    </table>
  </div>
</body>
</html>
```

### person.html
```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>개인정보 수정</title>
  <style>
    body {
      font-family: 'Noto Sans KR', sans-serif;
      background-color: #f2f2f2;
      margin: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .info-container {
      width: 100%;
      max-width: 400px;
      background-color: #fff;
      padding: 2rem;
      border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    }
    h2 {
      text-align: center;
      margin-bottom: 1.5rem;
    }
    form {
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }
    input {
      padding: 0.6rem;
      border: 1px solid #ccc;
      border-radius: 4px;
      font-size: 1rem;
    }
    button {
      padding: 0.6rem;
      background-color: #3498db;
      color: white;
      font-size: 1rem;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      transition: background-color 0.3s;
    }
    button:hover {
      background-color: #2980b9;
    }
  </style>
</head>
<body>
  <div class="info-container">
    <h2>개인정보 수정</h2>
    <form>
      <label for="name">이름</label>
      <input type="text" id="name" placeholder="이름 입력">
      <label for="email">이메일</label>
      <input type="email" id="email" placeholder="이메일 입력">
      <button type="button" onclick="location.href='board.html'">수정완료</button>
    </form>
  </div>
</body>
</html>
```

## 채점기준
```txt
UI 구현 표준 검토하기 CSS 분리 여부 :  외부 CSS 파일 사용 시 6점, style 태그 사용 시 3점, 미사용 시 0점

UI 구현 표준 검토하기 : 적절한 HTML 태그 대부분 사용 시 24점,  8점, 미작업 0점

UI 디자인 구현 능력 : 제시 레이아웃 90% 이상 일치 시 40점, 70% 32점, 50% 24점, 40% 16점, 30% 8점, 미작업 0점

유효성 점검 구현 입력 필드 유효성 메시지 8점 : 메시지 정상 출력 시 8점, 출력 오류 시 4점, 미작업 0점

JS 동작 처리 능력  : 경고창 + 커서이동 + submit 방지 3가지 모두 구현 시 16점, 2가지 12점, 1가지 8점, 미흡하나 시도 4점, 미작업 0점
```