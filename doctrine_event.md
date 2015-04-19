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
```xml
<service id="app.event_listener.file_listener" class="AppBundle\EventListener\FileListener">
    <tag name="doctrine.event_listener" event="preRemove"/>
</service>
```

```php
/**
 * @param LifecycleEventArgs $args Event arguments
 */
public function preRemove(LifecycleEventArgs $args)
{
    $entity = $args->getObject();

    if ($entity instanceof Photo) {
        $file = $entity->getFile();
        $file->delete();
    }
}
```
