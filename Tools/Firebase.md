# Firebase

## Firebase + React Setup

1. 리액트 프로젝트 생성
2. Firebase 프로젝트 생성
3. npm install firebase
4. firebase.js 생성

```
import { initializeApp } from "firebase/app";

const firebaseConfig = {
  apiKey: "",
  authDomain: "",
  projectId: "",
  storageBucket: "",
  messagingSenderId: "",
  appId: "",
};

const app = initializeApp(firebaseConfig);

export default app;

```

5. index.js import

```
import firebase from "firebase/compat/app";
```

6. .env 생성 (firebase key들을 환경변수로 설정, Github에 올라가지 않게)

```
// .env
REACT_APP_API_KEY = ...

// src/firebase.js
apiKey: process.env.REACT_APP_API_KEY,
```
