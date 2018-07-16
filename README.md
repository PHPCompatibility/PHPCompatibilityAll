[![License](https://poser.pugx.org/PHPCompatibility/phpcompatibility-all/license.png)](https://github.com/PHPCompatibility/PHPCompatibilityAll/blob/master/LICENSE)
[![Build Status](https://travis-ci.org/PHPCompatibility/PHPCompatibilityAll.png?branch=master)](https://travis-ci.org/PHPCompatibility/PHPCompatibilityAll)

# PHPCompatibilityAll

Convenience package to install all the external rulesets which the [PHPCompatibility organisation](https://github.com/PHPCompatibility) maintains, in one go using Composer.


## What's included in this package ?

### Base ruleset

- [![PHPCompatibility Current Version](https://poser.pugx.org/phpcompatibility/php-compatibility/v/stable.png)](https://packagist.org/packages/phpcompatibility/php-compatibility) [PHPCompatibility](https://github.com/PHPCompatibility/PHPCompatibility) - External PHPCS standard to check your codebase for PHP cross-version compatibility.

### Framework/CMS specific rulesets

- [![PHPCompatibilityJoomla Current Version](https://poser.pugx.org/phpcompatibility/phpcompatibility-joomla/v/stable.png)](https://packagist.org/packages/PHPCompatibility/phpcompatibility-joomla) [PHPCompatibilityJoomla](https://github.com/PHPCompatibility/PHPCompatibilityJoomla) - PHPCompatibility ruleset specific for Joomla projects.
- [![PHPCompatibilityWP Current Version](https://poser.pugx.org/phpcompatibility/phpcompatibility-wp/v/stable.png)](https://packagist.org/packages/PHPCompatibility/phpcompatibility-wp) [PHPCompatibilityWP](https://github.com/PHPCompatibility/PHPCompatibilityWP) - PHPCompatibility ruleset specific for WordPress projects.


## Requirements

* PHP 5.3+ for use with [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) 2.3.0+.
* PHP 5.4+ for use with [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) 3.0.2+.
* [Composer](https://getcomposer.org/)

Use the latest stable release of PHP_CodeSniffer for the best results.


## Installation instructions

If you don't have a Composer plugin installed to manage the `installed_paths` setting for PHP_CodeSniffer, run the following from the command-line:
```bash
composer require --dev dealerdirect/phpcodesniffer-composer-installer:^0.4.3 phpcompatibility/phpcompatibility-all:*
composer install
```

If you already have a Composer PHPCS plugin installed, run:
```bash
composer require --dev phpcompatibility/phpcompatibility-all:*
composer install
```

Next, run:
```bash
vendor/bin/phpcs -i
```
If all went well, you will now see that the PHPCompatibility, PHPCompatibilityJoomla and PHPCompatibilityWP standards are installed for PHP_CodeSniffer.


## How to use

Now you can use any of the following commands to inspect your code:
```bash
./vendor/bin/phpcs -p . --standard=PHPCompatibility
./vendor/bin/phpcs -p . --standard=PHPCompatibilityJoomla
./vendor/bin/phpcs -p . --standard=PHPCompatibilityWP
```

By default, you will only receive notifications about deprecated and/or removed PHP features.

To get the most out of the PHPCompatibility standards, you should specify a `testVersion` to check against. That will enable the checks for both deprecated/removed PHP features as well as the detection of code using new PHP features.
    - You can run the checks for just one specific PHP version by adding `--runtime-set testVersion 5.5` to your command line command.
    - You can also specify a range of PHP versions that your code needs to support. In this situation, compatibility issues that affect any of the PHP versions in that range will be reported: `--runtime-set testVersion 5.3-5.5`.
    - Since PHPCompatibility 7.1.3, you can omit one part of the range if you want to support everything above or below a particular version, i.e. use `--runtime-set testVersion 7.0-` to run all the checks for PHP 7.0 and above.

For more detailed information, see the README of the main [PHPCompatibility](https://github.com/PHPCompatibility/PHPCompatibility#sniffing-your-code-for-compatibility-with-specific-php-versions) standard.


## License

All code within the PHPCompatibility organisation is released under the GNU Lesser General Public License (LGPL). For more information, visit https://www.gnu.org/copyleft/lesser.html


## Changelog

### 1.0.0 - 2018-07-17

Initial release containing the PHPCompatibility, PHPCompatibilityJoomla and PHPCompatibilityWP rulesets.

