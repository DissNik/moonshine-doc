# Checkbox

- [Основы](#basics)
- [Создание](#make)
- [Значения вкл/выкл](#on-off)
- [Редактирование в режиме preview](#preview-edit)
- [Реактивность](#reactive)

---

<a name="basics"></a>
## Основы

Содержит все [базовые методы](/docs/{{version}}/fields/basic-methods).

Поле *Checkbox* - это поле для выбора значения типа да/нет.

<a name="make"></a>
## Создание

```php
use MoonShine\UI\Fields\Checkbox; 

Checkbox::make('Публиковать', 'is_publish') 
```

<a name="on-off"></a>
## Значения вкл/выкл

По умолчанию поле имеет значения `1` и `0` для выбранного и невыбранного состояний соответственно. Методы `onValue()` и `offValue()` позволяют переопределить эти значения.

```php
onValue(int|string $onValue)
```

```php
offValue(int|string $onValue)
```

```php
Checkbox::make('Публиковать', 'is_publish')
    ->onValue('yes')
    ->offValue('no')
```

<a name="editing-in-preview"></a>
## Редактирование в режиме preview

Метод `updateOnPreview()` позволяет редактировать поле *Checkbox* в режиме *предпросмотра*.

```php
updateOnPreview(?Closure $url = null, ?ResourceContract $resource = null, mixed $condition = null)
```

- `$url` - url для обработки асинхронного запроса,
- `$resource` - ресурс модели, на которую ссылается отношение,
- `$condition` - условие выполнения метода.

> [!TIP]
> Настройки не обязательны и должны быть переданы, если поле работает вне ресурса.

```php
Checkbox::make('Публичный')
    ->updateOnPreview()
```

// TODO simpleMode()

<a name="preview-edit"></a>
## Редактирование в режиме preview

Данному полю доступно [редактирование в режиме preview](/docs/{{version}}/fields/basic-methods.md#preview-edit).

<a name="reactive"></a>
## Реактивность

Данному полю доступна [реактивность](/docs/{{version}}/fields/basic-methods.md#reactive).