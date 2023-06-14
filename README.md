# Cookies and Sessions. Client-side example (Vue3)

In Vue 3, cookies and sessions are not specifically related to the framework itself but are concepts used in web development in general. Cookies and sessions are commonly used for managing user state and storing data between different requests and pages in a web application.

## Cookies:
Cookies are small pieces of data that are stored on the user's browser. They are typically used to store user-specific information, such as user preferences, login credentials, or tracking data. Cookies are sent from the server to the browser and are included in subsequent requests to the server.
To work with cookies in Vue 3, you can use the js-cookie library, which provides an easy way to read, write, and delete cookies. Here's an example of how to set and read a cookie using js-cookie in a Vue 3 component:

```vue
<template>
  <div>
    <button @click="setCookie">Set Cookie</button>
    <button @click="getCookie">Get Cookie</button>
  </div>
</template>

<script>
import Cookies from 'js-cookie';

export default {
  methods: {
    setCookie() {
      Cookies.set('myCookie', 'Hello, world!');
    },
    getCookie() {
      const value = Cookies.get('myCookie');
      console.log(value); // Output: Hello, world!
    }
  }
};
</script>
```

In this example, the setCookie method sets a cookie named "myCookie" with the value "Hello, world!". The getCookie method retrieves the value of the cookie and logs it to the console.

## Sessions:
Sessions are a way to store user-specific data on the server. A session typically involves the creation of a unique identifier (session ID) for each user, which is stored as a cookie on the user's browser. The server then uses this session ID to retrieve the associated session data.
In a Vue 3 application, you can work with sessions by using server-side technologies such as Node.js with a framework like Express.js or using session management libraries like express-session.

Here's a basic example of using express-session with a Vue 3 application:

```node
// server.js (Node.js with Express.js)
const express = require('express');
const session = require('express-session');

const app = express();

app.use(session({
  secret: 'mySecretKey',
  resave: false,
  saveUninitialized: true,
  cookie: { secure: false } // Change to 'true' if using HTTPS
}));

app.get('/set-session', (req, res) => {
  req.session.mySessionData = 'Hello, world!';
  res.send('Session set!');
});

app.get('/get-session', (req, res) => {
  const value = req.session.mySessionData;
  res.send(value);
});

app.listen(3000, () => {
  console.log('Server started on port 3000');
});
```

In this example, the server is configured to use express-session middleware. The /set-session endpoint sets a session data variable, and the /get-session endpoint retrieves the session data.

You can make HTTP requests from your Vue 3 application to these server endpoints to interact with the session data.

Note: This is a basic example to demonstrate the concept. In a real-world application, you would typically handle more complex session management, including authentication and session expiration.

Remember that cookies and sessions have their own security considerations, so it's essential to follow best practices and ensure you're handling sensitive data appropriately.

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
