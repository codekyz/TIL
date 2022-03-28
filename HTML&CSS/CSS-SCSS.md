# SCSS

- css 전처리기
- Scss가 Sass를 위한 공식적인 syntax로 릴리즈
- 따라서 Sass나 Scss는 거의 같은 것
- etc. stylus, less

## Variable

- 대표적인 사이즈, 컬러 등

```
// _variables.scss
$bg: #000000;

// styles.scss
import "_variables";
...
background: $bg;
...
```

## Nesting

```
.box {
  ...
  h1 {
    color: ...
  }
  button {
    color: ...
  }
  &:hover {
    color: ...
  }
}
```

## mixins

- 함수처럼 작동

```
// _mixins.scss
@mixin myTitle($color) {
  font-size: ...
  @if $color {
    color: $color
  } @else {
    color: blue;
  }
}

// styles.scss
import "_mixins";

h1{
  @include myTitle(red);
}
```

## Extends

- 같은 코드를 반복하고 싶지 않을 때

```
// _buttons.scss
%button {
  border-radius : ...
  ...
}

// styles.scss
import "_buttons";

button {
  @extend %button;
  ...
}

```

## gulp

- compile 하거나 transform해주는 node.js package
- scss or sass -> css
