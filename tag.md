doc: [a Working with Tagged Services](http://symfony.com/doc/current/components/dependency_injection/tags.html)

Symfony\Bundle\TwigBundle\DependencyInjection\Compiler\TwigEnvironmentPass::process

```php
$definition = $container->getDefinition('twig');
foreach ($container->findTaggedServiceIds('twig.extension') as $id => $attributes) {
    $definition->addMethodCall('addExtension', array(new Reference($id)));
}
```

Twig_Environment

```php
 public function addExtension(Twig_ExtensionInterface $extension)
  {
      $this->extensions[$extension->getName()] = $extension;
  }
```

src/AppBundle/Resources/config/services.xml

```xml
<service id="app.file.asset" class="AppBundle\Twig\FileExtension">
    <argument type="service" id="router"/>
    <tag name="twig.extension"/>
</service>
```
