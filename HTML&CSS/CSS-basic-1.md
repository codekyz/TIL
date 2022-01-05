[인프런 HTML5 & CSS3 기초 문법 올인원](https://inf.run/rjt5) / [개발자 이도해](https://www.youtube.com/channel/UCRf6ut93gIImnmdebqdPI9A)  

## 인라인, 인터널, 익스터널 방식
- 인라인 : 태그에 직접 스타일 작성
- 인터널 : style태그 내부에 스타일 작성
- 익스터널 : 별도에 파일에 스타일 작성
    - `<link rel="stylesheet" href="./style.css" />`

### 선택자
- 전체 선택자 : `*` html 모든 요소
- 태그 요소 선택자 : `tag name` 해당 모든 태그에 적용
- 아이디 선택자 : `#id`
- 클래스 선택자 : `.class`
- 결합 선택자 : `부모(띄어쓰기) 자손` 자손 요소 모두 선택 
                `부모 > 자식` 자식 요소만 선택

### 텍스트와 폰트 스타일
- 텍스트 : 컬러 `color` 정렬 `text-align` 줄간격 `line-height` 데코 `text-decoration`
- 폰트 : `font-size` `font-weight` `font-family`
- [구글 웹폰트](https://fonts.google.com/)  

### 링크와 리스트 스타일
- `a(선택자):hover(상태)`
- `list-style`

### 가상 선택자
> 실제로 존재하진 않지만 필요에 의해 임의로 지정해서 사용하는 선택자  
- ex) `hover` `focus` `active` 등
- 구조적인 가상 선택자
    - ex) `first-child` `last-child` `nth-child(3,even,odd)`

### 여백과 테두리 스타일
- 내부 여백 : `padding: 상하px 좌우px`
- 외부 여백 : `margin`
- 테두리 : `border` padding과 margin사이

### 박스 모델, 박스 모델 사이징
- 박스 모델의 width와 height는 내용만을 기준으로 함(테두리나 여백 포함x)
- `box-sizing: border-box` : 테두리를 기준으로 박스 모델 크기를 정함

### 디스플레이와 포지션
- 디스플레이display : HTML의 인라인, 블록 요소와 같음. 요소가 화면에서 어떻게 표현되는가 어떻게 위치하는가를 지정하는 속성(지정하지 않을 경우 HTML의 기본값을 따라감)
    - `none` : 표시X
    - `block` 
    - `inline` : `block`속성을 잃음 따라서 사이즈나 여백 지정 불가
    - `inline-block` : 블록 특성유지 인라인 처럼 동작 

- 포지션position
    - `static` : 기본값. HTML태그가 가지는 기본값
    - `fixed` : 뷰포트를 기준으로 위치를 지정. 웹 페이지 사이즈가 변하거나 스크롤이 생겨도 고정
    - `absolute` : 조상요소들 중 포지션이 `relative`로 지정된 가장 가까운 조상요소를 기준으로 위치를 정함(없을 경우 `body` 기준)
    - `relative` : 요소의 현재 위치를 기준으로 지정된 오프셋만큼 떨어져서 위치

## 플렉스 레이아웃 Flexbox
> 모던 CSS. 플렉스를 적용할 컨테이너와 플렉스 관련 속성이 적용되어 배치될 실제 아이템들로 구성
> 가로 또는 세로 단일 방향 레이아웃 배치에 적합
```
.container {
    display: flex;
}
```
- 축(Axis) : 메인 축(아이템이 배치된 방향의 축)과 교차 축(메인 축과 수직을 이루는 축)을 기준으로 아이템을 정렬
- 컨테이너 속성
    - `flex-direction: row(defalt) column` 
    - `flex-wrap` : 아이템 크기에 따른 줄바꿈 설정 
    - `flex-flow` : direction과 wrap의 축약형 
    - `justify-content: ` `center` `space-between` `space-around` : 메인 축의 정렬을 지정
    - `align-items`(높이 지정 필수) `stretch`(컨테이너 높이에 따라 늘어남) : 교차 축의 정렬을 지정
    - `align-content` : 줄바꿈이 활성화 되어있을때의 정렬
- 아이템 속성
    - `flex-basis` : 아이템의 기본크기를 지정하는데 메인 축 방향에 따라 결정됨 
    - `flex-grow`(기본값 0, 비율설정가능) : 아이템들이 flex-basis이상으로 늘어나는 값 
    - `flex-shrink`(기본값 1=줄어듬 0=줄어들지않음) : grow와 반대로 기본 값 이하로 줄어드는 값
    - `flex` : 축약형
    - `align-self` : 단일 아이템 자기 자신의 교차축 방향 정렬을 지정하는 속성
    - `order` : 배치 우선 순위

## 그리드 Grid
> 모던 CSS. 행과 열로 구성된 레이아웃을 배치하는데 적합한 기능
```
.container {
    display: grid;
}
```
- 컨테이너 속성
    - `grid-template-rows(columns) : repeat(auto-fill, minmax(200px, 1fr))` : 행과 열을 설정 (fr단위로 설정하면 비율, auto-fit은 남은 공간을 셀을 늘려서 채움)
    - `rows(columns)-gap` : 행열 여백
    - `grid-auto-rows(columns)` : 템플릿에서 벗어나는 컬럼에 적용
    - `justify-items` : 가로방향 정렬
    - `align-items` : 세로방향 정렬
    - `place-items` : 축약형
    - `  ''  -content` : 아이템들의 크기가 컨테이너 크기보다 작을때 정렬 방향 지정
- 아이템 속성
    - `grid-row(column)[-start(end)] : 셀 번호[1/3]` : 셀 병합처럼 아이템의 크기를 지정
    - `justify(align)-self` : 아이템 본인의 정렬
    - `order` : 배치 우선순위