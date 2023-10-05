# react에서 FontAwesome 아이콘 사용하기

[공식문서](https://fontawesome.com/v6/docs/web/use-with/react/)

> 버전6 기준 작성

1. Add SVG Core

```
npm i --save @fortawesome/fontawesome-svg-core
```

2. Add Icon Packages

```
# Free icons styles
npm i --save @fortawesome/free-solid-svg-icons
npm i --save @fortawesome/free-regular-svg-icons
```

3. Add the React Component

```
npm i --save @fortawesome/react-fontawesome@latest
```

4. Add the Icons to Your Project

```
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faBars } from "@fortawesome/free-solid-svg-icons";

<FontAwesomeIcon icon={faBars} size="2x" />

```
