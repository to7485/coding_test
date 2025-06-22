## App.js

```jsx
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import StackNavigation from '../src/navigation/StackNavigation';

const App = () => (
 <NavigationContainer>
   <StackNavigation />
 </NavigationContainer>
);

export default App;
```

## StackNavigation.js
```jsx
import React from 'react';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
import LoginScreen from '../screens/LoginScreen';
import SignupScreen from '../screens/SignupScreen';

const Stack = createNativeStackNavigator();

const StackNavigation = () => (
 <Stack.Navigator screenOptions={{ headerShown: false }}>
   <Stack.Screen name="Login" component={LoginScreen} />
   <Stack.Screen name="Signup" component={SignupScreen} />
 </Stack.Navigator>
);

export default StackNavigation;

```

## SignupScreen.js
```jsx
import React, { useState } from 'react';
import styled from 'styled-components/native';
import CustomInput from '../components/CustomInput';
import CustomButton from '../components/CustomButton';

const Container = styled.View`
 flex: 1;
 justify-content: center;
 align-items: center;
 padding: 20px;
`;

const Title = styled.Text`
 font-size: 28px;
 margin-bottom: 20px;
 font-weight: bold;
`;

const SignupScreen = ({ navigation }) => {
 const [name, setName] = useState('');
 const [email, setEmail] = useState('');
 const [password, setPassword] = useState('');

 return (
   <Container>
     <Title>회원가입</Title>
     <CustomInput placeholder="이름" value={name} onChangeText={setName} />
     <CustomInput placeholder="이메일" value={email} onChangeText={setEmail} />
     <CustomInput placeholder="비밀번호" value={password} onChangeText={setPassword} secureTextEntry />
     <CustomButton title="회원가입" onPress={() => console.log('회원가입 버튼 클릭')} />
     <CustomButton title="로그인" backgroundColor="#e67e22" onPress={() => navigation.navigate('Login')} />
   </Container>
 );
};

export default SignupScreen;
```

## LoginScreen.js

```jsx
import React, { useState } from 'react';
import styled from 'styled-components/native';
import CustomInput from '../components/CustomInput';
import CustomButton from '../components/CustomButton';

const Container = styled.View`
 flex: 1;
 justify-content: center;
 align-items: center;
 padding: 20px;
`;

const Title = styled.Text`
 font-size: 28px;
 margin-bottom: 20px;
 font-weight: bold;
`;

const LoginScreen = ({ navigation }) => {
 const [email, setEmail] = useState('');
 const [password, setPassword] = useState('');

 return (
   <Container>
     <Title>로그인</Title>
     <CustomInput placeholder="이메일" value={email} onChangeText={setEmail} />
     <CustomInput placeholder="비밀번호" value={password} onChangeText={setPassword} secureTextEntry />
     <CustomButton title="로그인" onPress={() => console.log('로그인 버튼 클릭')} />
     <CustomButton title="회원가입" backgroundColor="#2ecc71" onPress={() => navigation.navigate('Signup')} />
   </Container>
 );
};

export default LoginScreen;
```

## CustomInput.js
```jsx
import React from 'react';
import styled from 'styled-components/native';

const Input = styled.TextInput`
 width: 80%;
 padding: 12px;
 margin: 10px 0;
 border: 1px solid #ccc;
 border-radius: 8px;
`;

const CustomInput = ({ placeholder, value, onChangeText, secureTextEntry = false }) => (
 <Input
   placeholder={placeholder}
   value={value}
   onChangeText={onChangeText}
   secureTextEntry={secureTextEntry}
 />
);

export default CustomInput;
```

## CustomButton.js
```jsx
import React from 'react';
import styled from 'styled-components/native';

const Button = styled.TouchableOpacity`
 width: 80%;
 padding: 14px;
 background-color: ${({ backgroundColor }) => backgroundColor || '#3498db'};
 margin: 10px 0;
 border-radius: 8px;
 align-items: center;
`;

const ButtonText = styled.Text`
 color: white;
 font-size: 16px;
 font-weight: bold;
`;

const CustomButton = ({ title, onPress, backgroundColor }) => (
 <Button onPress={onPress} backgroundColor={backgroundColor}>
   <ButtonText>{title}</ButtonText>
 </Button>
);

export default CustomButton;
```