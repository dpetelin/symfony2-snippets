doc:[Creating the Subscriber Class](http://symfony.com/doc/current/cookbook/doctrine/event_listeners_subscribers.html#creating-the-subscriber-class)

```xml
<service id="app.event_listener.comment_listener" class="AppBundle\EventListener\CommentListener">
    <tag name="kernel.event_subscriber" />
</service>
```

AppBundle\EventListener\CommentListener

```php
public static function getSubscribedEvents()
{
    return [
        AppEvents::NOTIFICATION_COMMENT => 'addedComment',
        AppEvents::NOTIFICATION_ANSWER_FOR_COMMENT => 'addedAnswerForComment',
    ];
}

public function addedAnswerForComment(CommentEvent $event) {...}
public function addedComment(CommentEvent $event) {...}
```
