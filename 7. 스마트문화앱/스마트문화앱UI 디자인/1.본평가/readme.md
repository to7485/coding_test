## 다음 요구사항에 맞춰 React Native 앱을 설계하시오.

## 1. 프로젝트 생성하기
- 프로젝트명 : react-native-test
-  프로젝트는 다음과 같은 구성으로 작성해주세요

```
/src
├ components/
│   ├ CustomInput.js
│   └ CustomButton.js
├ screens/
│   ├ LoginScreen.js
│   └ SignupScreen.js
├ navigation/
│   └ StackNavigation.js
└ App.js
```

### 로그인과 회원가입 화면을 다음의 조건에 맞게 설계하시오
- 네비게이션
@react-navigation/native와 @react-navigation/native-stack 이용
 
### 1. 입력필드와 버튼을 재사용하도록 컴포넌트로 설계하세요.
#### CustomInput
- placeholder, value, onChangeText를 props로 받아 TextInput을 렌더링
- styled-components로 스타일 작성
- secureTextEntry props를 통해 비밀번호 입력 가능
- 다음의 스타일을 사용하세요
  
```
 width: 80%;
 padding: 12px;
 margin: 10px 0;
 border: 1px solid #ccc;
 border-radius: 8px;
```

#### CustomButton
- title, onPress props로 동작
- backgroundColor props로 색상 변경 가능
- styled-components로 스타일 작성
- 다음 스타일을 사용하세요

``` 
 width: 80%;
 padding: 14px;
 background-color: → props로 넘겨받은 색깔이 있으면 적용한다, 없으면 ‘#3498db’를 기본색으로 한다.
 margin: 10px 0;
 border-radius: 8px;
 align-items: center;
```

### 2. 로그인 화면과 회원가입 화면을 작성하세요
#### LoginScreen
- 헤더는 보이지 않게 설정 (headerShown: false)
- 이메일 입력 필드 (입력한 내용이 그대로 보여야 합니다.)
- 비밀번호 입력 필드 (입력하면 내용이 o로 나와야 합니다.)
- 로그인 버튼 (클릭 시 console.log('로그인 버튼 클릭'))
- "회원가입" 버튼 (클릭 시 SignupScreen 이동)

![img](./img/본평가_로그인.png)

#### SignupScreen
- 이메일 입력 필드
- 비밀번호 입력 필드 (입력하면 내용이 o로 나와야 합니다.)
- 이름 입력 필드
- 회원가입 버튼 (클릭 시 console.log('회원가입 버튼 클릭'))
- "로그인" 버튼 (클릭 시 LoginScreen 이동)

![img](./img/본평가_회원가입.png)