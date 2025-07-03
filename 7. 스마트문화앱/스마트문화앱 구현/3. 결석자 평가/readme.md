# 🎵 AlbumSearchApp 프로젝트 명세

## 📁 프로젝트 구조

```
AlbumSearchApp/
├── App.js
├── navigation/
│   └── StackNavigator.js
├── screens/
│   ├── SearchScreen.js
│   └── DetailScreen.js
├── components/
│   └── AlbumItem.js
├── api/
│   └── itunesApi.js
└── constants/
    └── apiConfig.js
```

---

## ⚙️ 구현 조건

- 화면 간 이동은 **React Navigation의 Stack Navigation** 사용
- API 호출은 **axios 또는 fetch** 사용 가능
- **API 키 필요 시 `apiConfig.js`에서 관리**
- **iTunes Search API** 사용:  
  [https://itunes.apple.com/search](https://itunes.apple.com/search)
- 필요한 외부 라이브러리는 **사전 설치 필요**

---

## 🔎 iTunes Search API 주요 파라미터

| 파라미터 | 설명 |
|----------|------|
| `term` | 검색어 (필수) |
| `country` | 국가 코드 (기본값: US) |
| `media` | 검색할 미디어 종류 (`music`, `movie`, `software` 등) |
| `entity` | 미디어의 하위 카테고리 (`album`, `musicTrack` 등) |
| `limit` | 최대 검색 결과 수 (기본값: 50, 최대: 200) |
| `lang` | 응답 언어 (`en_us`, `ko_kr` 등) |

---

## 🧩 기능 구현 요건

### ✅ SearchScreen.js

- 화면 상단에 **TextInput**과 **검색 버튼** 배치
- 사용자가 검색어 입력 후 버튼 클릭 시 **iTunes API를 통해 음악 앨범 검색**
- 결과는 **FlatList**를 통해 출력  
  (각 항목은 `AlbumItem` 컴포넌트 사용)
- 출력 내용:
  - 앨범명
  - 아티스트명
  - 앨범 이미지
- **앨범 클릭 시 상세화면으로 이동**
- 검색 실패 또는 결과 없음 시 `Alert` 표시

---

### ✅ DetailScreen.js

- 선택한 앨범의 정보 상세 표시
- 출력 항목:
  - 앨범 이미지
  - 앨범 이름
  - 아티스트명
  - 발매일
  - 장르
  - 트랙 수
- 전체 화면은 **ScrollView**로 구성