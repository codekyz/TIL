[HTML 태그들, 헷갈리는거 정리해 보았다 🥳 (시맨틱 태그, 중요한 태그들 모음)](https://youtu.be/T7h8O7dpJIg)  

# 시맨틱(의미있는) 태그

## 사용해야하는 이유
1. SEO(검색최적화)
2. Accessibility(웹 접근성 ex.스크린리더)
3. For us, Maintainability(유지보수성)

## 구조
```
<header>
    <nav></nav>
</header>
<main>
    <aside></aside>
    <article>
        <section></section>
    </article>
</main>
<footer>
</footer>
```

## article vs section
- `article` : main내에서 다른 내용들과 상관없이 독립적으로 고유 정보를 나타낼 때
- `section` : 연관있는 내용들을 하나로 묶어줄 때

## i vs em / b vs strong
- `i` : 시각적인 이탤릭체
- `em` : 강조하는 이탤릭체(스크린리더에서)
- `b` : 시각적인 볼드체
- `strong` : 강조하는 볼드체(스크린리더에서)

## button vs a
- `button` : 특정한 액션을 위해
- `a` : 어디론가 이동할 때