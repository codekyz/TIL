[만들면서 배우는 리액트:기초 - 진유림님](https://inf.run/eFeh)  

[React 공식문서](https://ko.reactjs.org/docs/add-react-to-a-website.html)  
[Ant Design](https://ant.design/components/overview/)  

## Component
- 시작은 대문자
- component는 함수를 통해 만듬(props)
- 사용자 정의 태그

## JSX
- JavaScript + XML
- HTML 태그 안에서 {}를 이용해서 js를 쓸 수 있음
- 변수에 담은 태그는 리액트 엘리먼드라고 부름
- onClick <- 대문자 주의

## 리액트 코드 브라우저에 그리기
```
// html
<div id="app"></div>

// react
ReactDOM.render(myelement, target);
```

## 스타일링
- className
- Inline : style={{속성: '스타일값'}}

#### CSS Library
[Emotion CSS](https://emotion.sh/docs/introduction)
[Tailwind CSS](https://tailwindcss.com/docs/installation)

## 이벤트핸들러
- 일반 js 이벤트 목록과 동일(중간 대문자 차이)
- `event.preventDefault();` : submit 후 refresh되는것을 막아줌(js문법)

#### 네이밍
- `onClick` -> `handle ~ Click`
- `onMouseOver` -> `handle ~ MouseOver`
- props로 넘길때는 `on ~ Click`

## 상태 useState
- 컴포넌트 안에서 자유롭게 변경할 값이 필요할 때
```
const [상태명, 상태변경함수명] = React.useState(초기값)
```

## 리스트
```
<ul>
    {favorites.map(image=> <img src={image}</img>)}
</ul>
```
- map : 자바 스크립트에서 배열을 순회하는 api

## useEffect
- ui를 새로 그릴때마다 App안에 모든 코드가 새로 호출됨
```
React.useEffect(() => {
    setInitialCat();
}, []);
```
- 두번째 인자로 빈 배열을 넘기면 처음 한번만
- 원하는 상태를 넘기면 상태가 업데이트 될 때마다 호출


## create-react-app
[React 공식문서](https://ko.reactjs.org/docs/create-a-new-react-app.html)  
- 리액트 초기 개발에 필요한 모든 것을 자동으로 해주는 라이브러리
    1. 간단한 앱 껍데기
    2. 리액트 라이브러리 셋업(개발용/프로덕션용)
    3. 웹팩 셋업(라이브 서버, 저장할때마다 jsx -> js)
    4. 테스트 셋업
    5. 빌드 셋업(js로 변환, 코드용량 최소화, 프로덕션 라이브러리 설정 등)
- 실무 개발환경
    - 프로덕션 버전 리액트 라이브러리 사용
    - 바벨 떼기(이미 통역된 js)
