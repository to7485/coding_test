# ✅ AlbumSearchApp 정답 예시

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

## 📄 App.js

```jsx
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import StackNavigator from './navigation/StackNavigator';

export default function App() {
  return (
    <NavigationContainer>
      <StackNavigator />
    </NavigationContainer>
  );
}
```

---

## 📄 navigation/StackNavigator.js

```jsx
import React from 'react';
import { createStackNavigator } from '@react-navigation/stack';
import SearchScreen from '../screens/SearchScreen';
import DetailScreen from '../screens/DetailScreen';

const Stack = createStackNavigator();

export default function StackNavigator() {
  return (
    <Stack.Navigator>
      <Stack.Screen name="Search" component={SearchScreen} options={{ title: '앨범 검색' }} />
      <Stack.Screen name="Detail" component={DetailScreen} options={{ title: '상세 정보' }} />
    </Stack.Navigator>
  );
}
```

---

## 📄 constants/apiConfig.js

```js
export const ITUNES_BASE_URL = 'https://itunes.apple.com/search';
```

---

## 📄 api/itunesApi.js

```js
import axios from 'axios';
import { ITUNES_BASE_URL } from '../constants/apiConfig';

export const searchAlbums = async (query) => {
  try {
    const response = await axios.get(ITUNES_BASE_URL, {
      params: {
        term: query,
        entity: 'album',
        limit: 25,
      },
    });
    return response.data.results;
  } catch (error) {
    console.error(error);
    return [];
  }
};
```

---

## 📄 components/AlbumItem.js

```jsx
import React from 'react';
import { View, Text, Image, Pressable, StyleSheet } from 'react-native';

export default function AlbumItem({ album, onPress }) {
  return (
    <Pressable onPress={onPress} style={styles.container}>
      <Image source={{ uri: album.artworkUrl100 }} style={styles.image} />
      <View style={styles.info}>
        <Text style={styles.title}>{album.collectionName}</Text>
        <Text style={styles.artist}>{album.artistName}</Text>
      </View>
    </Pressable>
  );
}

const styles = StyleSheet.create({
  container: { flexDirection: 'row', marginBottom: 12 },
  image: { width: 60, height: 60, marginRight: 10 },
  info: { flex: 1 },
  title: { fontWeight: 'bold' },
  artist: { color: '#555' },
});
```

---

## 📄 screens/SearchScreen.js

```jsx
import React, { useState } from 'react';
import { View, TextInput, Button, FlatList, StyleSheet, Alert } from 'react-native';
import AlbumItem from '../components/AlbumItem';
import { searchAlbums } from '../api/itunesApi';

export default function SearchScreen({ navigation }) {
  const [query, setQuery] = useState('');
  const [albums, setAlbums] = useState([]);

  const handleSearch = async () => {
    if (!query.trim()) {
      Alert.alert('검색어를 입력하세요');
      return;
    }
    const results = await searchAlbums(query);
    if (results.length === 0) {
      Alert.alert('검색 결과가 없습니다');
    }
    setAlbums(results);
  };

  return (
    <View style={styles.container}>
      <View style={styles.searchRow}>
        <TextInput
          style={styles.input}
          placeholder="가수 또는 앨범명"
          value={query}
          onChangeText={setQuery}
        />
        <Button title="검색" onPress={handleSearch} />
      </View>
      <FlatList
        data={albums}
        keyExtractor={(item) => item.collectionId.toString()}
        renderItem={({ item }) => (
          <AlbumItem
            album={item}
            onPress={() => navigation.navigate('Detail', { album: item })}
          />
        )}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 10 },
  searchRow: { flexDirection: 'row', marginBottom: 10 },
  input: { flex: 1, borderWidth: 1, padding: 8, marginRight: 10 },
});
```

---

## 📄 screens/DetailScreen.js

```jsx
import React from 'react';
import { View, Text, Image, ScrollView, StyleSheet } from 'react-native';

export default function DetailScreen({ route }) {
  const { album } = route.params;

  return (
    <ScrollView contentContainerStyle={styles.container}>
      <Image source={{ uri: album.artworkUrl100 }} style={styles.image} />
      <Text style={styles.title}>{album.collectionName}</Text>
      <Text style={styles.text}>아티스트: {album.artistName}</Text>
      <Text style={styles.text}>발매일: {album.releaseDate.substring(0, 10)}</Text>
      <Text style={styles.text}>장르: {album.primaryGenreName}</Text>
      <Text style={styles.text}>트랙 수: {album.trackCount}</Text>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: { padding: 16 },
  image: { width: '100%', height: 200, resizeMode: 'contain' },
  title: { fontSize: 22, fontWeight: 'bold', marginBottom: 10 },
  text: { fontSize: 16, marginBottom: 6 },
});
```