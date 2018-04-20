---
title: "CSS Counters"
date: 2018-02-08T00:45:55+03:00
draft: false
menu: "main"
---
На чистом CSS мы можем подсчитывать количество чего-либо на странице, выводить это количество, проставлять порядковые номера. Не нужно писать никакого JS и это отлично [поддерживается](https://caniuse.com/#feat=css-counters)

# Нумеруем заголовки

Нужно проставить порядковый номер перед каждым заголовком? Проще простого! Допустим, структура следующая:
```
<section>
  <h1>Овощи</h1>
</section>

<section>
  <h1>Фрукты</h1>
</section>
```

Чтобы браузер самостоятельно проделал за нас рутинную работу и пронумеровал заголовки, пишем следующие стили
```
body {
  /* создаём/обнуляем счетчик по имени section */
  counter-reset: section;
}
h1::before {
  /* выводим счётчик в псевдоэлементе */
  content: counter(section) '. ';
  /* инкрементируем его */
  counter-increment: section;
}
```

В итогде получаем:

<p data-height="265" data-theme-id="light" data-slug-hash="yjNGeq" data-default-tab="result" data-user="vloginov" data-embed-version="2" data-pen-title="CSS Counters 1" class="codepen">See the Pen <a href="https://codepen.io/vloginov/pen/yjNGeq/">CSS Counters 1</a> by Vadim (<a href="https://codepen.io/vloginov">@vloginov</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

Как это работает?
Сначала нужно счётчик создать. В данном случае мы делаем это в body.
Затем счетчик инкрементируется каждый раз при создании псевдоэлемента заголовка. Там же и выводится.

# Двухуровневая нумерация

Что если мы хотим получить такое?

---
### 1. Овощи
- 1.1. Помидоры
- 1.2. Огурцы
- 1.3. Капуста

### 2. Фрукты
- 2.1. Яблоки
- 2.2. Груши
- 2.3. Бананы

---

Нужно всего-лишь использовать два счетчика. Полный пример:

<p data-height="421" data-theme-id="light" data-slug-hash="GdJPpj" data-default-tab="html,result" data-user="vloginov" data-embed-version="2" data-pen-title="CSS Counters" class="codepen">See the Pen <a href="https://codepen.io/vloginov/pen/GdJPpj/">CSS Counters</a> by Vadim (<a href="https://codepen.io/vloginov">@vloginov</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

Логика та же, появилась лишь дополнительная переменная `section-item`, которая обнуляется в каждом разделе. Таким образом, у каждого раздела свой отсчёт.

Если бы я знал это раньше, не стал бы мучиться с пробросом $index переменной из родительского repeat во вложенный на Angular.js, а сделал бы на чистом CSS, сэкономив время и не засоряя код. Ученье - свет 😉