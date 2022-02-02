## Vuex 셋팅
```
npm install vuex@next
```

## main.js
```
import { createApp } from 'vue';
import App from './App.vue';
import store from './store/index';

createApp(App).use(store).mount('#app')
```

## store/index.js
```
import { createStore } from 'vuex';

export default createStore({
    state: {

    },
    getters: {

    },
    mutations: {

    },
    actions: {

    },
});
```
