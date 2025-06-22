## App.js

```js
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

## navigation/StackNavigator.js
```js
import React from 'react';
import { createStackNavigator } from '@react-navigation/stack';
import SearchScreen from '../screens/SearchScreen';
import DetailScreen from '../screens/DetailScreen';

const Stack = createStackNavigator();

const StackNavigator = () => {
  return (
    <Stack.Navigator>
      <Stack.Screen name="Search" component={SearchScreen} options={{ title: '도서 검색' }} />
      <Stack.Screen name="Detail" component={DetailScreen} options={{ title: '상세 정보' }} />
    </Stack.Navigator>
  );
};

export default StackNavigator;
```

## api/naverApi.js
```js
import axios from 'axios';
import { NAVER_CLIENT_ID, NAVER_CLIENT_SECRET } from '../constants/apiConfig';

export const searchBooks = async (query) => {
  try {
    const res = await axios.get('https://openapi.naver.com/v1/search/book.json', {
      params: { query, display: 20 },
      headers: {
        'X-Naver-Client-Id': NAVER_CLIENT_ID,
        'X-Naver-Client-Secret': NAVER_CLIENT_SECRET,
      },
    });

    return res.data.items.map((item) => ({
      title: item.title.replace(/<[^>]*>/g, ''),
      author: item.author,
      price: item.discount,
      image: item.image,
      description: item.description,
      isbn: item.isbn,
    }));
  } catch (error) {
    console.error(error);
    return [];
  }
};
```

## constants/apiConfig.js
```js
export const NAVER_CLIENT_ID = 'MyOtXjysC6JFxy2J3FIo';
export const NAVER_CLIENT_SECRET = 'lcPw7L4jHA';
```

## components/BookItem.js
```js
import React from 'react';
import { View, Text, Image, Pressable, StyleSheet } from 'react-native';

const BookItem = ({ book, onPress }) => {
  return (
    <Pressable onPress={onPress} style={styles.container}>
      <Image source={{ uri: book.image }} style={styles.thumbnail} />
      <View style={styles.info}>
        <Text style={styles.title}>{book.title}</Text>
        <Text style={styles.author}>{book.author}</Text>
      </View>
    </Pressable>
  );
};

const styles = StyleSheet.create({
  container: { flexDirection: 'row', marginBottom: 12 },
  thumbnail: { width: 60, height: 90, marginRight: 10 },
  info: { flex: 1 },
  title: { fontWeight: 'bold' },
  author: { color: '#555' },
});

export default BookItem;
```

## screens/SearchScreen.js
```js
import React, { useState } from 'react';
import { View, TextInput, Button, FlatList, StyleSheet, Alert } from 'react-native';
import BookItem from '../components/BookItem';
import { searchBooks } from '../api/naverApi';

const SearchScreen = ({ navigation }) => {
  const [query, setQuery] = useState('');
  const [books, setBooks] = useState([]);

  const handleSearch = async () => {
    try {
      const results = await searchBooks(query);
      if (results.length === 0) {
        Alert.alert('검색 결과가 없습니다.');
      }
      setBooks(results);
    } catch {
      Alert.alert('네트워크 오류가 발생했습니다.');
    }
  };

  return (
    <View style={styles.container}>
      <View style={styles.searchRow}>
        <TextInput
          style={styles.input}
          placeholder="검색어를 입력하세요"
          value={query}
          onChangeText={setQuery}
        />
        <Button title="검색" onPress={handleSearch} />
      </View>
      <FlatList
        data={books}
        keyExtractor={(item) => item.isbn}
        renderItem={({ item }) => (
          <BookItem book={item} onPress={() => navigation.navigate('Detail', { book: item })} />
        )}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: { flex: 1, padding: 10 },
  searchRow: { flexDirection: 'row', marginBottom: 10 },
  input: { flex: 1, borderWidth: 1, borderColor: '#ccc', padding: 8, marginRight: 10 },
});

export default SearchScreen;
```

## screens/DetailScreen.js
```js
import React from 'react';
import { View, Text, Image, ScrollView, StyleSheet } from 'react-native';

const DetailScreen = ({ route }) => {
  const { book } = route.params;

  return (
    <ScrollView contentContainerStyle={styles.container}>
      <Image source={{ uri: book.image }} style={styles.image} />
      <Text style={styles.title}>{book.title}</Text>
      <Text style={styles.author}>저자: {book.author}</Text>
      <Text style={styles.price}>가격: {book.price}</Text>
      <Text style={styles.description}>{book.description}</Text>
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  container: { padding: 16 },
  image: { width: '100%', height: 300, resizeMode: 'contain' },
  title: { fontSize: 22, fontWeight: 'bold', marginTop: 16 },
  author: { marginTop: 8, fontSize: 16 },
  price: { marginTop: 4, fontSize: 16 },
  description: { marginTop: 12, fontSize: 14, lineHeight: 20 },
});

export default DetailScreen;
```