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
