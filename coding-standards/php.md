**Note: This page is under construction. Please check back later.**

# PHP Coding Standards for KygekTeam Projects

## Example

```php
<?php

declare(strict_types=1);

namespace KygekTeam\example;

use Exception;

class ExampleClass {
    
    // Constants MUST be before properties and methods
    public const CONSTANT_ONE = "ExampleString";
    public const CONSTANT_TWO = 6415;
    
    // Properties MUST be after constants, yet before methods
    /** @var bool */
    public $propertyOne = true;
    /** @var string[]|null */
    private $propertyTwo;
    
    // Methods MUST be after properties and constants
    /**
     * @throws Exception
     * @param string $string  Should not be empty
     * @param bool $output    Whether to echo ExampleClass->propertyTwo (default is false)
     * @return callable
     */
    public function exampleMethod(string $string, bool $output = false) : callable {
        if (empty($string)) {
            throw new Exception("First parameter should not be an empty string!");
        }
        
        switch ($string) {
            case "StringOne":
                $this->propertyTwo = [
                    "SomeVeryLongStringThatArrayShouldBeSplitAcrossMultipleLines-One",
                    "SomeVeryLongStringThatArrayShouldBeSplitAcrossMultipleLines-Two",
                    "SomeVeryLongStringThatArrayShouldBeSplitAcrossMultipleLines-Three"
                ];
                break;
                                  // Prefer splitting switch case statements with a blank line to improve readability
            case "StringTwo":
            case "StringThree":
                $this->propertyOne = false;
                break;
                
            default:
                $this->propertyTwo = [self::CONSTANT_ONE, "ShortString"];
        }
        
        if ($output && $this->propertyTwo !== null) { // Prefer using strict comparison whenever possible
            echo implode(PHP_EOL, $this->propertyTwo);
        }
        
        $someVar = self::CONSTANT_TWO;
        return function (int $int = 6415) use ($someVar) : bool {
            return $int === $someVar;
        }
    }
    
    /**
     * @return string[]|null
     */
    public function getPropertyTwo() : ?array {
        return $this->propertyTwo;
    }
    
}
```
