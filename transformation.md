```php
class CategoriesToIdsTransformer implements DataTransformerInterface
{
    /**
     * @var ObjectManager
     */
    protected $om;

    /**
     * Form constructor
     *
     * @param \Doctrine\Common\Persistence\ObjectManager $om
     *
     */
    public function __construct(ObjectManager $om)
    {
        $this->om = $om;
    }

    /**
     * @inheritdoc
     */
    public function transform($value)
    {
        if (null === $value) {
            return '';
        }

        $collection = $value instanceof Collection ? $value->toArray() : $value;

        $ids = array_map(function ($entity) {
            return $entity->getId();
        }, $collection);

        return implode(',', $ids);
    }

    /**
     * @inheritdoc
     */
    public function reverseTransform($value)
    {
        if (!$value) {
            return null;
        }

        $ids = explode(',', $value);

        $categories = $this->om
            ->getRepository('AppBundle:Category')
            ->findAllByIds($ids);

        if (empty($categories)) {
            throw new TransformationFailedException(sprintf(
                'A Categories with ids "%s" does not exist!',
                $value
            ));
        }

        return $categories;
    }
}
```

```php
$builder->addModelTransformer(new CategoriesToIdsTransformer($this->om));
```
