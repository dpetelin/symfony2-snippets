Динамическое добавления элементв для событи FormEvents::PRE_SET_DATA

```php
public function preSetData(FormEvent $event)
{
    $form = $event->getForm();
    $data = $event->getData();
    if ($data->getType() !== null) {
        $form->add('parameter');
    }
}
```

Удаляем элемент если не нужно маппить данные для соотвествующего поля в моделе 
(для события FormEvents::POST_SUBMIT )

```php
public function preSubmit(FormEvent $event)
{
    $requestData = $event->getData();
    $modelData = $event->getForm()->getData();
    if ($requestData['number'] > $modelData->getNumber()) {
        $form = $event->getForm();
        $form->remove('phone');
    }
}
```
