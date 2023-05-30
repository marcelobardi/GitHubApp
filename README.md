# GitHubApp
import React, { useState } from 'react';
import { StyleSheet, Text, View, TextInput, Button } from 'react-native';

export default function App() {
  const [username, setUsername] = useState('');
  const [userData, setUserData] = useState(null);

  const fetchUserData = async () => {
    try {
      const response = await fetch(`https://api.github.com/users/${username}`);
      const data = await response.json();
      setUserData(data);
    } catch (error) {
      console.error(error);
    }
  };

  return (
    <View style={styles.container}>
      <Text style={styles.title}>GitHub App</Text>
      <TextInput
        style={styles.input}
        placeholder="Enter GitHub username"
        value={username}
        onChangeText={setUsername}
      />
      <Button title="Fetch User Data" onPress={fetchUserData} />
      {userData && (
        <View style={styles.userData}>
          <Text style={styles.username}>{userData.login}</Text>
          <Text>Name: {userData.name}</Text>
          <Text>Location: {userData.location}</Text>
          <Text>Followers: {userData.followers}</Text>
          <Text>Repositories: {userData.public_repos}</Text>
        </View>
      )}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: 16,
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 16,
  },
  input: {
    width: '100%',
    height: 40,
    borderWidth: 1,
    borderColor: '#ccc',
    borderRadius: 4,
    paddingHorizontal: 8,
    marginBottom: 8,
  },
  userData: {
    marginTop: 16,
  },
  username: {
    fontSize: 20,
    fontWeight: 'bold',
    marginBottom: 8,
  },
});
