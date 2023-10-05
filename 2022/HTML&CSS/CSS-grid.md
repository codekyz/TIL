# grid

- flexbox로는 grid를 구현하기 힘들어서 나오게 됨
- grid-template-columns : 만들고 싶은 column의 수 만큼 크기를 작성
- grid-template-rows : 원하는 row의 크기를 작성
- grid-template-areas : grid-area와 함께 사용, layout을 string으로 작성
- grid-template : (shortcuts)
  ```
  grid-template :
    "header header header header" 1fr
    "content content content nav" 2fr
    "footer footer footer footer" 1fr / 1fr 1fr 1fr 1fr
    // repeat dosen't work
  ```

---

- repeat(반복횟수, 크기);
  - auto-fit : 정해진 사이즈 안에서 현재 element를 딱 맞게 채움
  - auto-fill : 정해진 사이즈 안에서 가능한 많은 element를 생성(비어있더라도)
- fr(fraction) : 사용가능한 공간(grid내에서)
- minmax(100px, 1fr) : 최소 크기와 최대 크기를 지정
- min-content : content가 작아질 수 있는 만큼 작아짐
- max-content : content가 필요한 크기만큼 가짐

```
repeat(auto-fit, minmax(20px, max-content))
```

---

- column-gap : column사이의 공간
- row-gap : row사이의 공간
- gap : column과 row사이의 공간

---

- 높이와 넓이가 있어야 적용됨
- items는 각 셀에 대한 속성
- justify-items : stretch(default) (수평, 가로)
- align-items : stretch(default) (수직, 세로)
  - place-items : 수직 수평

---

- content는 grid 자체를 움직이는 속성
- justify-content : start(default) 수평
- align-content : start(default) 수직
  - place-content : 수직 수평

---

- 설정된 것 이상으로 셀이 늘어나면 적용되는 속성
- grid-auto-rows
- grid-auto-flow : row or column(늘어날 방향을 적용)
- grid-auto-columns
-

# 자식속성

- grid-area : grid-template-areas에서 사용할 이름을 지정해줌

---

- grid-column-start(end) : 어디서 시작하고 어디서 끝날지 숫자 **(column line)** 로 지정
- grid-row-start(end) : 어디서 시작하고 어디서 끝날지 숫자 **(row line)** 로 지정
  - grid-column : start / end
  - grid-row : start / end
    - (-1) = 가장 끝 라인을 의미
    - span 2 = 공간 2개를 의미

---

- justify-self
- align-self
  - place-self : 수직 수평
