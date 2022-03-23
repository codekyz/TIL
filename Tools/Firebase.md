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

## Authentication

[공식문서](https://firebase.google.com/docs/reference/js/auth.md?authuser=1&hl=ko#auth_package)

```
// fbase.js
import { getAuth } from "firebase/auth";
...
export const authService = getAuth();
```

- createUserWithEmailAndPassword(authService, email, password) : 메일과 패스워드로 인증하는 사용자 계정을 만듬
- signInWithPopup(aushService, provider) : 인증 제공자가 제공하는 정보를 통해 인증
- signOut(authService) : 현재 사용자를 로그아웃

## Firestore

[공식문서](https://firebase.google.com/docs/reference/js/firestore_.md?authuser=1&hl=en#@firebase/firestore)

- NoSQL Database로 유연함, 제한사항이 있음(자유도 낮음)
- Database > Collection : 폴더 > Document : 문서

```
// doc 생성
const onSubmit = async (event) => {
  event.preventDefault();
  await addDoc(collection(dbService, "tweets"), {
    tweet,
    createAt: Date.now(),
  });
  setTweet("");
};

// doc 가져오기
const getTweets = async () => {
  const dbTweets = await getDocs(collection(dbService, "tweets"));
  dbTweets.forEach((document) => {
    const tweetObj = {
      ...document.data(),
      id: document.id,
    };
    setTweets((prev) => [tweetObj, ...prev]);
  });
};

or
// onSnapshot을 이용하면 db에 변동사항이 생길때마다 갱신(listener)
useEffect(() => {
  onSnapshot(collection(dbService, "tweets"), (snapshot) => {
    const tweetArray = snapshot.docs.map((doc) => ({
      id: doc.id,
      ...doc.data(),
    }));
    setTweets(tweetArray);
  });
}, []);

// doc 삭제
await deleteDoc(doc(dbService, "tweets", `${tweetObj.id}`));

// doc 업데이트
await updateDoc(doc(dbService, "tweets", `${tweetObj.id}`), {
  text: newTweet,
});
```
