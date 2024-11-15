# Assets

Компонент **Assets** используется для подключения к html-странице скриптов и таблиц стилей, 
добавленные через [AssetManager](/docs/{{version}}/appearance/assets).

> [!NOTE]
> Компонент **Assets** так же подключает системные стили и скрипты.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Layout\Assets;

Assets::make(); 
```
tab: Blade
```blade
<x-moonshine::layout.assets />
```
~~~

> [!TIP]
> Родительский компонент: [head](/docs/{{version}}/components/head)