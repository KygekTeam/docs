# PHP Coding Standards for KygekTeam Projects

This documentation applies to all PHP source code modifications in all of KygekTeam projects (commits, pull requests, etc). We enforce a **very high standard** for coding standards to ensure maxiumum consistency and readability. Failing to meet our standards will result in the rejection of PHP source code modification. Please read and see our example before modifying PHP source code(s) belonging to KygekTeam.

## Standards

KygekTeam uses [PSR-1](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md) as standard for PHP projects with some exceptions:

- Opening braces MUST go on the same line and MUST have spaces before.
- Control structure keywords or opening braces MUST have one space before or after them.
- Long arrays SHOULD be split across multiple lines, where each subsequent line is indented once.
- Files MUST use only the `<?php` tag.
- Files MUST NOT have an ending `?>` tag.
- Code MUST use 4 (four) spaces for indenting.
- Code MUST use namespaces where namespaces is required.
- Strings SHOULD use the double quote `"` except when the single quote is required.
- Strict types (`declare(strict_types=1)`) MUST be enabled in all files.
- All constant, property and method declarations SHOULD be preceded by a visibility modifier.
- Constants MUST be before properties and methods.
- Properties MUST be after constants, yet before methods.
- Methods MUST be after properties and constants.
- Classes body MUST start and end with a blank line.
- Blank lines MAY not be indented.
- PHPDoc SHOULD be used when declaring unsupported parameter/return type. (This includes defining property types)
- PHPDoc SHOULD be used when a method throws an exception.

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
For an example of a plugin which applies the standards above, please see [KygekExamplePlugin](https://github.com/KygekTeam/KygekExamplePlugin) plugin.
