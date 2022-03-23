# display

- block : 넓이와 높이를 가짐
- inline-block : block 속성을 가지면서 inline 속성을 유지
- inline : 넓이와 높이를 가질 수 없음, 유동적(ex. text)

# flexbox

- 자식요소를 컨트롤 하기위해서는 flexbox container(부모요소)가 필요(display: flex)
- Main Axis (justify-content) : 기본값은 row(행)
- Cross Axis (align-items)
- flex-direction: (기본값은 row)
- flex-wrap: wrap (자식의 사이즈를 유지, 기본값은 nowrap);
- align-content: (element가 아닌 line에 관한 속성, 줄바꿈이 일어났을때)

## 자식 속성

- align-self : 자식요소가 가지는 Cross Axis 정렬 속성
- order : 기본값은 0 (html을 바꿀수 없을때 유용)
- flex-shrink : 기본값은 1 (지정한 크기보다 작아질 때 값을 지정, 클수록 더 작아짐)
- flex-grow : 기본값은 0 (여분의 공간만큼 더 크게 만듬, 클수록 더 커짐)
- flex-basis : element에게 기본 크기를 주는 것, main axis 쪽 크기(grow,shrink가 적용되긴 전)
