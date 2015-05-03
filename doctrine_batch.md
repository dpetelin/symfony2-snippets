```php
$q = $em->createQuery('select u from AppBundle\Entity\User u');
$iterableResult = $q->iterate();
foreach ($q->iterate() as $row) {
    $user = $row[0];
    // detach from Doctrine, so that it can be Garbage-Collected immediately
    $em->detach($user);
}
```
