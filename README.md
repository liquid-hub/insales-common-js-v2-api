# Шпаргалка по JS API InSales v2 на платформе InSales

Commonjs добавляет на сайт следущие модули:

* [EventBus](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/EventBus.md)
* [Cart](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Cart.md)
* [Products](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Products.md)
* [AjaxSearch](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/AjaxSearch.md)
* [Compare](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Compare.md)
* [Template](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Template.md)
* [ajaxAPI](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/ajaxAPI.md)
* [Shop](https://github.com/liquid-hub/insales-common-js-v2-api/blob/master/Shop.md)


## Подключение

Для подключения JS API InSales v2 необходимо прописать настройку в settings_data.json — "common_js_version": "v2".

Файл settings_data.json не доступен через бэк-офис, поэтому новое свойство нужно добавлять вручную через скачивание темы и последующей установке с новыми параметрами. Так же файл можно поправить если для разработки вы используете — [InSales-uploader](https://insales.github.io/insales-uploader/).

Пример `settings_data.json`:
```json
{
  "common_js_version": "v2",
  "presets": {
    "custom": {
      "color_text_primary": "#222222",
      "font_size_primary": "16px"
    }
  },
  "theme_title": "Базовый шаблон"
}
```
