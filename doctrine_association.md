One-To-Many, Bidirectional
```php
class Product
{
    /**
     * @OneToMany(targetEntity="Feature", mappedBy="product")
     **/
    private $features;

    public function __construct() {
        $this->features = new ArrayCollection();
    }
}
```
