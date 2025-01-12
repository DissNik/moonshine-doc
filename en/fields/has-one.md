# HasOne

- [Basics](#basics)
- [Fields](#fields)
- [Parent ID](#parent-id)
- [Modification](#modify)

---

<a name="basics"></a>
## Basics

The *HasOne* field is designed to work with the same named relationship in Laravel and includes all [Basic methods](/docs/{{version}}/fields/basic-methods).

To create this field, use the static method `make()`.

```php
HasMany::make(
    Closure|string $label,
    ?string $relationName = null,
    Closure|string|null $formatted = null,
    ModelResource|string|null $resource = null,
)
```

- `$label` - the label, title of the field,
- `$relationName` - the name of the relationship,
- `$resource` - the model resource that the relationship refers to.

> [!CAUTION]
> The `$formatted` parameter is not used in the `HasMany` field!

> [!WARNING]
> Having a model resource that the relationship refers to is mandatory.
The resource must also be [registered](/docs/{{version}}/resources#define) in the `MoonShineServiceProvider` service provider in the `$core->resources()` method. Otherwise, there will be a 500 error (Resource is required for MoonShine\Laravel\Fields\Relationships\HasOne...).

```php
HasOne::make('Profile', 'profile', resource: ProfileResource::class) 
```

![has_one](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/has_one.png)

![has_one_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/has_one_dark.png)

If you do not specify `$relationName`, the relationship name will be automatically determined based on `$label` (following camelCase rules).

```php
class ProfileResource extends ModelResource
{
    //...
}
//...
HasMany::make('Profile', 'profile')
```

You can omit `$resource` if the model resource matches the name of the relationship.

```php
class ProfileResource extends ModelResource
{
    //...
}
//...
HasMany::make('Profile')
```

<a name="fields"></a>
## Fields

The `fields()` method allows you to specify which fields will be involved in the *preview* or in the form building.

```php
fields(FieldsContract|Closure|iterable $fields)
```

```php
use MoonShine\UI\Fields\Relationships\HasOne;
use MoonShine\UI\Fields\Phone;
use MoonShine\UI\Fields\Text;

HasOne::make('Contacts', resource: ContactResource::class)
    ->fields([
        Phone::make('Phone'),
        Text::make('Address'),
    ]) 
```

![has_one_preview](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/has_one_preview.png)

![has_one_preview_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/has_one_preview_dark.png)

<a name="parent-id"></a>
## Parent ID

If the relationship has a resource, and you want to get the parent item's ID, you can use the *ResourceWithParent* trait.

```php
use MoonShine\Resources\ModelResource;
use MoonShine\Traits\Resource\ResourceWithParent;

class PostImageResource extends ModelResource
{
    use ResourceWithParent;
    //...
}
```

When using the trait, you need to define the following methods:

```php
protected function getParentResourceClassName(): string
{
    return PostResource::class;
}

protected function getParentRelationName(): string
{
    return 'post';
}
```

To get the parent ID, use the `getParentId()` method.

```php
$this->getParentId();
```

<a name="modify"></a>
## Modification

### Preview

The `modifyTable()` method allows you to change the *TableBuilder* for the preview.

```php
HasOne::make('Comment', resource: CommentResource::class)
    ->modifyTable(
        fn(TableBuilder $table) => $table
    )
```

### Form

The `modifyForm()` method allows you to change the *FormBuilder* for editing.

```php
HasOne::make('Comment', resource: CommentResource::class)
    ->modifyForm(
        fn(FormBuilder $form) => $form->submit('Custom title')
    )
```

### Redirect after modification

The `redirectAfter()` method allows for redirection after saving/adding/deleting.

```php
HasOne::make('Comment', resource: CommentResource::class)
    ->redirectAfter(fn(int $parentId) => route('home'))
```