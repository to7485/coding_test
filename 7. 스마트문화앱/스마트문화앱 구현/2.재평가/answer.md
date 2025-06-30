# 🎬 MovieSearchApp 전체 코드 정리

---

## `/constants/apiConfig.js`

```javascript
export const OMDB_API_KEY = 'your_api_key_here'; // 실제 키로 교체
```

---

## `/api/omdbApi.js`

```javascript
import axios from 'axios';
import { OMDB_API_KEY } from '../constants/apiConfig';

export const searchMovies = async (query) => {
  try {
    const res = await axios.get('https://www.omdbapi.com/', {
      params: {
        s: query,
        apikey: OMDB_API_KEY,
        type: 'movie',
      },
    });

    return res.data.Search || [];
  } catch (error) {
    console.error(error);
    return [];
  }
};
```

---

## `/App.js`

```javascript
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

## `/navigation/StackNavigator.js`

```javascript
import React from 'react';
import { createStackNavigator } from '@react-navigation/stack';
import SearchScreen from '../screens/SearchScreen';
import DetailScreen from '../screens/DetailScreen';

const Stack = createStackNavigator();

export default function StackNavigator() {
  return (
    <Stack.Navigator>
      <Stack.Screen name="Search" component={SearchScreen} />
      <Stack.Screen name="Detail" component={DetailScreen} />
    </Stack.Navigator>
  );
}
```

---

## `/components/MovieItem.js`

```javascript
import React from 'react';
import { View, Text, Image, Pressable, StyleSheet } from 'react-native';

export default function MovieItem({ movie, onPress }) {
  return (
    <Pressable onPress={onPress} style={styles.container}>
      <Image source={{ uri: movie.Poster }} style={styles.image} />
      <View style={styles.info}>
        <Text style={styles.title}>{movie.Title}</Text>
        <Text>{movie.Year}</Text>
      </View>
    </Pressable>
  );
}

const styles = StyleSheet.create({
  container: { flexDirection: 'row', marginBottom: 10 },
  image: { width: 60, height: 90, marginRight: 10 },
  info: { justifyContent: 'center' },
  title: { fontWeight: 'bold' },
});
```

---

## `/screens/SearchScreen.js`

```javascript
import React, { useState } from 'react';
import { View, TextInput, Button, FlatList, StyleSheet, Alert } from 'react-native';
import MovieItem from '../components/MovieItem';
import { searchMovies } from '../api/omdbApi';

export default function SearchScreen({ navigation }) {
  const [query, setQuery] = useState('');
  const [movies, setMovies] = useState([]);

  const handleSearch = async () => {
    if (!query.trim()) {
      Alert.alert('검색어를 입력하세요');
      return;
    }
    const results = await searchMovies(query);
    if (results.length === 0) {
      Alert.alert('검색 결과가 없습니다');
    }
    setMovies(results);
  };

  return (
    <View style={styles.container}>
      <View style={styles.searchRow}>
        <TextInput
          style={styles.input}
          placeholder="영화 제목을 입력하세요"
          value={query}
          onChangeText={setQuery}
        />
        <Button title="검색" onPress={handleSearch} />
      </View>
      <FlatList
        data={movies}
        keyExtractor={(item) => item.imdbID}
        renderItem={({ item }) => (
          <MovieItem
            movie={item}
            onPress={() => navigation.navigate('Detail', { movie: item })}
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

## `/screens/DetailScreen.js`

```javascript
import React from 'react';
import { View, Text, Image, ScrollView, StyleSheet } from 'react-native';

export default function DetailScreen({ route }) {
  const { movie } = route.params;

  return (
    <ScrollView contentContainerStyle={styles.container}>
      <Image source={{ uri: movie.Poster }} style={styles.image} />
      <Text style={styles.title}>{movie.Title}</Text>
      <Text style={styles.text}>연도: {movie.Year}</Text>
      <Text style={styles.text}>ID: {movie.imdbID}</Text>
      <Text style={styles.text}>타입: {movie.Type}</Text>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: { padding: 16 },
  image: { width: '100%', height: 300, resizeMode: 'contain' },
  title: { fontSize: 22, fontWeight: 'bold', marginTop: 16 },
  text: { fontSize: 16, marginTop: 8 },
});
```
