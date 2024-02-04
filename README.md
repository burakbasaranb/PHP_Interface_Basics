# PHP Interface Basics

## 1. What is an interface in PHP?

An interface in programming serves as a contract or a blueprint that defines a set of methodsthat a class must implement.

- Every function declared in an interface must be public; this is the nature of an interface.
- Every class that implements an interface must have these functions and its' variables.

### Declare the interface 'Template'
```php
interface Template
{
    /**
     * Set a variable in the template.
     *
     * @param string $name Variable name.
     * @param mixed  $var  Variable value.
     * 
     * @return void
     */
    public function setVariable($name, $var);

    /**
     * Get HTML output based on the template.
     *
     * @param string $template Template string.
     * 
     * @return string  Processed HTML.
     */
    public function getHtml($template);
}
```

## 2. How to implement an interface in PHP?

Classes should have the same methods (functions) and variables as the interface, which is Template.

### WorkingTemplate Class

Implementation of the Template interface.

```php
class WorkingTemplate implements Template
{
    /**
     * Holds template variables
     *
     * @var array Holds template variables.
     */
    private $_vars = [];

    /**
     * Set a variable in the template.
     *
     * @param string $name Variable name.
     * @param mixed  $var  Variable value.
     * 
     * @return void
     */
    public function setVariable($name, $var)
    {
        $this->_vars[$name] = $var;
    }

    /**
     * Get HTML output based on the template.
     *
     * @param string $template Template string.
     *
     * @return string  Processed HTML.
     */
    public function getHtml($template)
    {
        foreach ($this->_vars as $name => $value) {
            $template = str_replace('{' . $name . '}', $value, $template);
        }

        return $template;
    }
}
```

## 3. How to use?

Print the output of the WorkingTemplate class.

### Usage of WorkingTemplate

```php
$template = new WorkingTemplate();
$template->setVariable('name', 'John Doe');
$html = $template->getHtml('Hello, {name}!');
echo $html; // Output: Hello, John Doe!
```
