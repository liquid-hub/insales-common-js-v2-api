# Живой поиск по сайту

<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>

## Интерфейс

> Для быстрого создания интерфейсов в commonjs предусмотрены готовые обработчики форм.

> Обработчики ссылаются на data-атрибуты. В data-атрибуты пробрасывается информация из liquid.


### Назначение атрибутов

<details>
<summary>Подробнее</summary>

|Атрибут|Назначение|Расположение|
|-|-|-|
|data-search-field|Поле для ввода поискового запроса|Тег form|
|data-search-result|Блок в который записывается результат поиска|Тег form|
|[name="lang"]|Текущий язык|Тег form|


```twig
<form action="/search" method="get">
  <input type="hidden" name="lang" value="{{ language.locale }}">
  <input type="text" name="q" value="" placeholder="Поиск" data-search-field />
  <button type="submit">Поиск</button>
  <div data-search-result></div>
</form>
```

</details>

---

### Разметка для поиска

<details>
<summary>Подробнее</summary>

```twig
<form action="/search" method="get">
  <input type="hidden" name="lang" value="{{ language.locale }}">
  <input type="text" name="q" value="" placeholder="Поиск" data-search-field />
  <button type="submit">Поиск</button>
  <div data-search-result></div>
</form>
```
</details>

---

## Методы

### :hammer: setConfig

> Обновление настроек

<details>
<summary>:memo: Пример</summary>

```js
/**
 * @param {number} letters с какого символа начинать поиск
 * @param {number} delay задержка между запросами
 */

 AjaxSearch.setConfig({
   letters: 3,
   delay: 300
 });
```
</details>

<details>
<summary>:loudspeaker: События</summary>

> События класса EventBus

* before:insales:search -	Событие срабатывает перед любым взаимодействием с компонетом поиск
* update:insales:search -	Событие срабатывает после обновления результатов поиска
* always:insales:search -	Событие срабатывает после любого взаимодействия с компонетом поиск


```js
EventBus.subscribe('update:insales:search', function (data) {
  console.log('Товар добавлен');
});
```
</details>


<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>
