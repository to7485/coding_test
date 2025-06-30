## login.html
```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>로그인</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <div class="container">
    <a href="http://koreaisacademy.com/" target="_blank">
      <img src="logo.png" alt="로고" class="logo" />
    </a>

    <form id="loginForm">
      <div class="form-group">
        <label for="userId">아이디</label>
        <input type="text" id="userId" placeholder="아이디 입력" autofocus />
        <small class="error" id="idError"></small>
      </div>

      <div class="form-group">
        <label for="password">비밀번호</label>
        <input type="password" id="password" placeholder="비밀번호 입력" />
        <small class="error" id="pwError"></small>
      </div>

      <button type="submit">로그인</button>
    </form>
  </div>

  <script src="script.js"></script>
</body>
</html>
```

## style.css
```css
body {
  font-family: Arial, sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}

.container {
  width: 300px;
  text-align: center;
}

.logo {
  width: 64px;
  height: 64px;
  margin-bottom: 20px;
}

.form-group {
  margin-bottom: 15px;
  text-align: left;
}

input {
  width: 100%;
  padding: 8px;
  box-sizing: border-box;
}

button {
  width: 100%;
  padding: 10px;
  background-color: #3498db;
  color: white;
  border: none;
  cursor: pointer;
}

.error {
  color: red;
  font-size: 12px;
  margin-top: 4px;
  display: block;
}
```

script.js
```js
document.getElementById("userId").addEventListener("blur", function () {
  const id = this.value;
  const idError = document.getElementById("idError");
  const regex = /^[a-z0-9]{4,20}$/;

  if (!regex.test(id)) {
    idError.textContent = "아이디는 소문자와 숫자 조합의 4~20자여야 합니다.";
  } else {
    idError.textContent = "";
  }
});

document.getElementById("password").addEventListener("blur", function () {
  const pw = this.value;
  const pwError = document.getElementById("pwError");
  const count = [
    /[a-z]/.test(pw),
    /[A-Z]/.test(pw),
    /\d/.test(pw),
    /[!@#$%^&*]/.test(pw),
  ].filter(Boolean).length;

  if (pw.length < 8 || pw.length > 20 || count < 3) {
    pwError.textContent = "비밀번호는 8~20자이며 3종류 이상 포함해야 합니다.";
  } else {
    pwError.textContent = "";
  }
});

document.getElementById("loginForm").addEventListener("submit", function (e) {
  e.preventDefault();
  if (confirm("로그인 하시겠습니까?")) {
    alert("로그인 완료");
  }
});
```

## 채점기준
```txt
HTML - 로고 및 링크	상단 중앙에 64x64 크기 로고 배치, 클릭 시 지정 URL 이동	5점
HTML - 입력 필드 구성	아이디, 비밀번호 필드 포함 및 placeholder 사용	5점
HTML - label 태그 연결	for/id 속성으로 label 연결	5점
HTML - 자동 포커싱	페이지 로딩 시 아이디 입력창에 autofocus 적용	5점
HTML - 버튼 배치	입력 필드 아래에 버튼 위치	5점
CSS - 폼 중앙 정렬	로그인 폼이 수직·수평 중앙에 배치	5점
CSS - 입력/버튼 스타일	버튼, 입력창에 기본 스타일 지정	5점
CSS - 오류 메시지 스타일	에러 메시지에 빨간 글씨, 작은 크기 적용	5점
CSS - 전체 일관성	전체 UI 요소 정렬과 스타일 일관성 유지	5점
JS - 아이디 유효성 검사	정규식 검사, blur 이벤트, 에러 메시지 출력	15점
JS - 비밀번호 유효성 검사	8~20자, 3종 이상 포함 검사, blur 처리 및 에러 메시지 출력	15점
JS - 버튼 동작 처리	confirm/alert 동작, preventDefault() 처리	20점
```