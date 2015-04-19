Controller

```php
$this->get('event_dispatcher')->dispatch(
    AppEvents::NOTIFICATION_ANSWER_FOR_COMMENT,
    new CommentEvent(
        $this->getUser(),
        $entity,
        $parent
    )
);
```

Event

```php
namespace AppBundle\Event;

use Symfony\Component\EventDispatcher\Event;

class CommentEvent extends Event {...}
```
```xml
<service id="app.event_listener.comment_listener" class="AppBundle\EventListener\CommentSubscriber">
    <tag name="kernel.event_subscriber" />
    <argument type="service" id="app.mailer" />
</service>
```
CommentSubscriber

```php
    public static function getSubscribedEvents()
    {
        return [
            AppEvents::NOTIFICATION_COMMENT => 'addedComment',
            AppEvents::NOTIFICATION_ANSWER_FOR_COMMENT => 'addedAnswerForComment',
        ];
        
        public function addedAnswerForComment(CommentEvent $event)
        public function addedComment(CommentEvent $event)
    }
    
    
```
