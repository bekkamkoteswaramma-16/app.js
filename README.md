import React, { useState } from 'react';
import { View, Text, TextInput, Button, StyleSheet, Alert } from 'react-native';
import axios from 'axios';

export default function App() {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');

  const login = async () => {
    try {
      const res = await axios.post('http://YOUR_PC_IP:5000/api/auth/login', {
        email, password
      });
      Alert.alert("Success", "Welcome " + res.data.name);
      // Tarwata Dashboard ki navigate cheyyali
    } catch (error) {
      Alert.alert("Error", error.response.data.message);
    }
  }

  return (
    <View style={styles.container}>
      <Text style={styles.title}>House Rent Login</Text>
      <TextInput style={styles.input} placeholder="Email" onChangeText={setEmail} value={email}/>
      <TextInput style={styles.input} placeholder="Password" secureTextEntry onChangeText={setPassword} value={password}/>
      <Button title="Login" onPress={login} />
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: 'center', padding: 20 },
  title: { fontSize: 24, fontWeight: 'bold', textAlign: 'center', marginBottom: 20 },
  input: { borderWidth: 1, borderColor: '#ccc', padding: 10, marginBottom: 10, borderRadius: 5 }
});
