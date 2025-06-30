# 🎬 MovieSearchApp

OMDb API를 활용한 React Native 영화 검색 앱

---

## 📁 폴더 구조

```
MovieSearchApp/
├── App.js
├── navigation/
│   └── StackNavigator.js
├── screens/
│   ├── SearchScreen.js
│   └── DetailScreen.js
├── components/
│   └── MovieItem.js
├── api/
│   └── omdbApi.js
└── constants/
    └── apiConfig.js
```

---

## 🔧 설치해야 할 주요 라이브러리

```bash
npm install @react-navigation/native @react-navigation/native-stack
npm install react-native-screens react-native-safe-area-context
npm install axios
```

---

## 🔐 OMDb API Key 발급

1. [https://www.omdbapi.com/apikey.aspx](https://www.omdbapi.com/apikey.aspx) 접속  
2. 이메일 입력 → 무료 플랜 선택  
3. 인증 메일 확인 후 API Key 발급  

---

## 🔑 API 파라미터 요약

| 파라미터 | 용도   | 설명                                                                 |
|----------|--------|----------------------------------------------------------------------|
| s        | 검색   | 제목을 포함하는 영화 리스트 검색                                     |
| i        | 상세   | IMDb ID로 단일 영화 상세정보 조회                                   |
| t        | 상세   | 영화 제목으로 단일 영화 상세정보 조회                               |
| type     | 공통   | movie, series, episode 중 하나                                       |
| y        | 공통   | 연도 필터링                                                          |
| plot     | 상세   | short 또는 full 줄거리 길이 지정                                     |
| r        | 공통   | 응답 포맷(json, xml) 지정                                            |
| page     | 검색   | 페이징 (1~100, 10개씩)                                               |
| tomatoes | 상세   | Rotten Tomatoes 평점 포함 (true)                                     |
| callback | 공통   | JSONP 사용 시 콜백 이름                                              |
| apikey   | 공통   | 발급받은 API Key (필수)                                              |

✅ 요청 예시  
```
https://www.omdbapi.com/?apikey=YOUR_API_KEY&s=Avengers
```

---

## 📲 기능 구현 요건

### 🔍 `screens/SearchScreen.js`

- `TextInput`과 `검색 버튼` 구성
- 영화 제목 입력 후 검색 시 OMDb API 호출
- 결과를 `FlatList`로 출력 (제목, 연도, 포스터)
- 리스트 항목은 `MovieItem` 컴포넌트 사용
- 항목 클릭 시 `DetailScreen`으로 이동
- 예외 처리: 검색 결과 없음, 에러 발생 등

---

### 📄 `screens/DetailScreen.js`

- 선택한 영화 상세 정보 표시
- 표시 항목:
  - 제목
  - 감독
  - 줄거리
  - 개봉일
  - 포스터
- `ScrollView`로 감싸서 스크롤 가능하게 구현

---

## 🧩 각 파일 설명

### `App.js`

- `StackNavigator`를 통해 전체 앱 라우팅 정의

### `navigation/StackNavigator.js`

- `SearchScreen`, `DetailScreen` 포함한 네비게이션 설정

### `components/MovieItem.js`

- FlatList의 항목으로 사용
- 영화 포스터, 제목, 연도 표시
- 터치 시 상세 페이지로 이동

### `api/omdbApi.js`

- axios를 활용한 OMDb API 호출 함수 정의

### `constants/apiConfig.js`

- 발급받은 API 키를 상수로 분리하여 관리

```js
// 예시: constants/apiConfig.js
export const API_KEY = "YOUR_API_KEY";
```

---

📦 완성된 프로젝트는 React Native Expo 또는 CLI 환경에서 테스트 가능합니다.  
코드 전체가 필요하시면 파일별 소스도 제공 가능합니다. 요청해주세요!
