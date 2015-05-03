One-To-Many, Bidirectional
Inverse Side
```php
class Product
{
    /**
     * @OneToMany(targetEntity="Feature", mappedBy="product", 
     *   cascade={"persist"}, orphanRemoval=true
     *   )
     **/
    private $features;

    public function __construct() {
        $this->features = new ArrayCollection();
    }
    
    public function addFeature(Feature $feature)
    {
        $feature->setProduct($this);
        
        $this->features[] = $feature;

        return $this;
    }
}
```
Owning Side
```php
class Feature
{
    // ...
    /**
     * @ManyToOne(targetEntity="Product", inversedBy="features")
     * @JoinColumn(name="product_id", referencedColumnName="id", onDelete="CASCADE")
     **/
    private $product;
    
    public function setProduct(Product $product)
    {
        $this->product = $product
    }
}
```
