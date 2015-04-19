```xml
<service id="app.event_listener.user_listener" class="AppBundle\EventListener\UserListener">
    <tag name="doctrine.event_listener" event="onFlush"/>
</service>
```

```php
/**
 * @param OnFlushEventArgs $args Event arguments
 */
public function onFlush(OnFlushEventArgs $args)
{
    $em  = $args->getEntityManager();
    $uow = $em->getUnitOfWork();

    foreach ($uow->getScheduledEntityUpdates() as $entity) {
        if (!($entity instanceof User
            && in_array('isEnabled', array_keys($uow->getEntityChangeSet($entity))))
        ) {
            continue;
        }
        $args->getEntityManager()->getRepository('AppBundle:Comment')->updateEnabledForUser($entity);
    }
}
```
