```php
    /**
     * @param GetResponseForControllerResultEvent $event A GetResponseForControllerResultEvent instance
     */
    public function onKernelView(GetResponseForControllerResultEvent $event)
    {
        if (($container = $this->containerService->getContainer()) !== null) {
            $parameters = $event->getControllerResult();
            $parameters['container'] = $container;
            $event->setControllerResult($parameters);
        }
    }
```
