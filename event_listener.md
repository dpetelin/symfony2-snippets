doc: [a How to Create an Event Listener](http://symfony.com/doc/2.3/cookbook/service_container/event_listener.html)

```xml
<service id="app.event_listener.domain_listener" class="AppBundle\EventListener\DomainListener">
    <argument type="service" id="security.context" />
    <tag name="kernel.event_listener" event="kernel.request" method="onCheck" />
</service>
```

AppBundle\EventListener\DomainListener

```php
public function onCheck(Event $event)
{
    $user = $this->getUser();

    if (!$user) {
        return;
    }

    if (($this->securityContext->isGranted(RoleType::ROLE_SUPER_ADMIN) && $subDomain !== null)) {
        $this->securityContext->setToken(null);
        $event->setResponse(new Response('Access Denied', 403)); //propagation is stopped
    }
}
```
