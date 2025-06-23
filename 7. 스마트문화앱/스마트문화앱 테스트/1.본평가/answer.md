## src/App.js
```js
import React, { useState } from 'react';
import { View, Text, StyleSheet, ScrollView, Button, Alert } from 'react-native';
import FormInput from './components/FormInput';

export default function App() {
  const [email, setEmail] = useState('');
  const [emailError, setEmailError] = useState('');

  const [username, setUsername] = useState('');
  const [usernameError, setUsernameError] = useState('');

  const [password, setPassword] = useState('');
  const [passwordError, setPasswordError] = useState('');

  const [name, setName] = useState('');
  const [nameError, setNameError] = useState('');

  const validateRequired = (value, setError) => {
    if (value.trim() === '') {
      setError('필수 입력 항목입니다.');
      return false;
    }
    return true;
  };

  const validateEmail = (text) => {
    setEmail(text);
    if (!validateRequired(text, setEmailError)) return;

    const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    setEmailError(regex.test(text) ? '' : '올바른 이메일 형식이 아닙니다.');
  };

  const validateUsername = (text) => {
    setUsername(text);
    if (!validateRequired(text, setUsernameError)) return;

    const regex = /^[a-z0-9]{4,20}$/;
    setUsernameError(regex.test(text) ? '' : '아이디는 소문자와 숫자 조합의 4~20자여야 합니다.');
  };

  const validatePassword = (text) => {
    setPassword(text);
    if (!validateRequired(text, setPasswordError)) return;

    const lengthCheck = text.length >= 6 && text.length <= 20;
    const hasLetter = /[a-zA-Z]/.test(text);
    const hasNumber = /[0-9]/.test(text);
    const hasSpecial = /[!@#$%^&*]/.test(text);
    const typesMatched = [hasLetter, hasNumber, hasSpecial].filter(Boolean).length;

    const isValid = lengthCheck && typesMatched >= 2;

    setPasswordError(
      isValid ? '' : '비밀번호는 6~20자이며, 영문/숫자/특수문자 중 2가지 이상 포함해야 합니다.'
    );
  };

  const validateName = (text) => {
    setName(text);
    if (!validateRequired(text, setNameError)) return;

    const regex = /^[가-힣a-zA-Z]{1,30}$/;
    setNameError(regex.test(text) ? '' : '이름은 한글 또는 영문 1~30자여야 합니다.');
  };

  const handleSubmit = () => {
    validateEmail(email);
    validateUsername(username);
    validatePassword(password);
    validateName(name);

    if (
      email &&
      username &&
      password &&
      name &&
      !emailError &&
      !usernameError &&
      !passwordError &&
      !nameError
    ) {
      Alert.alert(
        '회원가입 정보',
        `이메일: ${email}\n아이디: ${username}\n비밀번호: ${password}\n이름: ${name}`
      );
    } else {
      Alert.alert('입력 오류', '모든 입력값을 올바르게 작성해주세요.');
    }
  };

  return (
    <ScrollView contentContainerStyle={styles.container}>
      <Text style={styles.header}>회원가입</Text>

      <FormInput
        placeholder="이메일"
        value={email}
        onChangeText={validateEmail}
        onBlur={() => validateEmail(email)}
        error={emailError}
        keyboardType="email-address"
      />

      <FormInput
        placeholder="아이디"
        value={username}
        onChangeText={validateUsername}
        onBlur={() => validateUsername(username)}
        error={usernameError}
      />

      <FormInput
        placeholder="비밀번호"
        value={password}
        onChangeText={validatePassword}
        onBlur={() => validatePassword(password)}
        error={passwordError}
        secureTextEntry
      />

      <FormInput
        placeholder="이름"
        value={name}
        onChangeText={validateName}
        onBlur={() => validateName(name)}
        error={nameError}
      />

      <View style={styles.buttonContainer}>
        <Button title="가입하기" onPress={handleSubmit} />
      </View>
    </ScrollView>
  );
```

## components/FormInput.js
```js
import React from 'react';
import { View, Text, TextInput, StyleSheet } from 'react-native';

const FormInput = ({
  value,
  placeholder,
  onChangeText,
  onBlur,
  error,
  secureTextEntry = false,
  keyboardType = 'default',
}) => {
  return (
    <View style={styles.inputWrapper}>
      <TextInput
        style={styles.input}
        placeholder={placeholder}
        value={value}
        onChangeText={onChangeText}
        onBlur={onBlur}
        secureTextEntry={secureTextEntry}
        keyboardType={keyboardType}
        autoCapitalize="none"
      />
      {error !== '' && <Text style={styles.error}>{error}</Text>}
    </View>
  );
};

const styles = StyleSheet.create({
  inputWrapper: {
    marginBottom: 10,
  },
  input: {
    borderColor: '#ccc',
    borderWidth: 1,
    borderRadius: 8,
    padding: 12,
  },
  error: {
    color: 'red',
    marginTop: 5,
  },
});

export default FormInput;
```