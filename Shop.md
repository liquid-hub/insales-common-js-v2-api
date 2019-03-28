# Вспомогательные методы

<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>

## Методы

> Методы объекта `Shop`

### :hammer: Shop.money.format

> Форматирование входной строки к виду, согласно настройкам БО

<details>
<summary>:memo: Параметры</summary>

```js
/*
* @param {string|number} amount - строка или число, которое надо отформатировать в валюту
*
* @return {string} Строка, содержащая результат форматирования
*/

Shop.money.format(1234.00);
// 1234 руб.
```
</details>
<details>
<summary>:computer: Пример</summary>

```js
Shop.money.format(1234.00);
// 1234 руб.
```
</details>

---

### :hammer: Shop.config.getProducId()

> Получить product-id на странице товара

<details>
<summary>:computer: Пример</summary>

```js
Shop.config.getProducId();
// на странице товара вернет -> "70513124"
// на остальных страницах -> null
```
</details>

---

---

### :hammer: Shop.config.get()

> Получить конфигурацию

<details>
<summary>:computer: Пример</summary>

```js
Shop.config.get();
```
</details>

---



<p align="right">
 <a href="https://github.com/liquid-hub/insales-common-js-v2-api">
 :arrow_left: Назад</a>
</p>



