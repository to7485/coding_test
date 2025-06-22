# React Native를 사용하여 다음과 같은 기능의 도서 검색 앱을 구현하시오.

- 프로젝트명: react-native-book

---

## 조건

### 디렉토리 구조

BookSearchApp/
├── App.js
├── navigation/
│ └── StackNavigator.js
├── screens/
│ ├── SearchScreen.js
│ └── DetailScreen.js
├── components/
│ └── BookItem.js
├── api/
│ └── naverApi.js
└── constants/
└── apiConfig.js


- 화면 간 이동은 Stack Navigation을 사용하여 구현한다.
- API 호출 시 사용하는 클라이언트 ID와 시크릿 키는 외부 파일(apiConfig.js)로 분리하여 관리한다.
- api의 요청은 axios, fetch 어느걸 사용해도 상관 없다.
- 필요한 라이브러리는 설치 후 진행한다.
- axios, @react-navigation/native, @react-navigation/stack



## 1. SearchScreen.js

- 상단에 검색창(TextInput) 과 검색 버튼(Button) 을 배치한다.
- 사용자가 검색어를 입력하고 검색 버튼을 누르면, 네이버 도서 검색 API를 통해 도서 목록을 가져온다.
- 검색 결과는 FlatList를 사용하여 제목, 저자, 이미지 정보로 목록 형태로 보여준다.
- FlatList에 들어갈 내용은 BookItem이라는 컴포넌트로 만들어서 사용한다.
- 도서 항목을 클릭하면 상세 정보 화면(DetailScreen) 으로 이동한다.
- 검색 결과가 없거나 네트워크 오류가 발생한 경우를 고려하여 에러 처리 및 사용자 피드백을 제공한다.( Alert을 띄우세요)

![img](../img/스마트문화앱%20구현_검색전.png) ![img](../img/스마트문화앱%20구현_검색후.png)


## 2. DetailScreen.js

- 상세 정보 화면에는 다음 정보들이 표시되어야 한다:
  - 도서 이미지
  - 도서 제목
  - 저자
  - 가격
  - 설명
- 설명이 길어지면 화면을 스크롤 할 수 있도록 한다.

![img](../img/스마트문화앱%20구현_상세페이지.png)

