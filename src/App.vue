<template>
  <div>
    <h1>{{ isLoggedIn ? `Welcome, ${username}!` : "Login" }}</h1>
    <button v-if="isLoggedIn" @click="logout">Logout</button>
    <form v-else @submit.prevent="login">
      <input
        type="text"
        v-model="credentials.username"
        placeholder="Username"
      />
      <input
        type="password"
        v-model="credentials.password"
        placeholder="Password"
      />
      <button type="submit">Login</button>
    </form>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import axios from "axios";

// Create a custom Axios instance with the base URL
const api = axios.create({
  baseURL: "http://localhost:3000",
});

const isLoggedIn = ref(false);
const username = ref("");
const credentials = ref({ username: "", password: "" });

// Function to set a cookie
const setCookie = (name: string, value: any, days: number) => {
  const expires = new Date();
  expires.setTime(expires.getTime() + days * 24 * 60 * 60 * 1000);
  document.cookie = `${name}=${value};expires=${expires.toUTCString()};path=/`;
};

// Function to get a cookie by name
const getCookie = (name: string | any[]) => {
  const cookies = document.cookie.split(";");
  for (let i = 0; i < cookies.length; i++) {
    const cookie = cookies[i].trim();
    if (cookie.startsWith(name + "=")) {
      return cookie.substring(name.length + 1);
    }
  }
  return null;
};

// Function to delete a cookie by name
const deleteCookie = (name: string) => {
  document.cookie = `${name}=;expires=Thu, 01 Jan 1970 00:00:00 UTC;path=/;`;
};

// Function to log in and create a session
const login = async () => {
  try {
    const response = await api.post("/api/login", credentials.value);
    const sessionToken = response.data.sessionToken;
    api.defaults.headers.common["Authorization"] = `Bearer ${sessionToken}`;
    setCookie("sessionToken", sessionToken, 7);
    isLoggedIn.value = true;
    username.value = credentials.value.username;
    credentials.value = { username: "", password: "" };
  } catch (error) {
    // Handle login error
  }
};

// Function to log out and destroy the session
const logout = async () => {
  try {
    await api.post("/api/logout");
    delete api.defaults.headers.common["Authorization"];
    deleteCookie("sessionToken");
    isLoggedIn.value = false;
    username.value = "";
  } catch (error) {
    // Handle logout error
  }
};

// Check if the user is already logged in
const sessionToken = getCookie("sessionToken");
if (sessionToken) {
  api.defaults.headers.common["Authorization"] = `Bearer ${sessionToken}`;
  isLoggedIn.value = true;
  // Fetch the user's information if needed
}

// Other logic...
</script>
