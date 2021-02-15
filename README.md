[![License](https://poser.pugx.org/PHPCompatibility/phpcompatibility-all/license.png)](https://github.com/PHPCompatibility/PHPCompatibilityAll/blob/master/LICENSE)
[![Build Status](https://github.com/PHPCompatibility/PHPCompatibilityAll/workflows/Validate/badge.svg?branch=master)](https://github.com/PHPCompatibility/PHPCompatibilityAll/actions)

# PHPCompatibilityAll

Convenience package to install all the external PHP_CodeSniffer rulesets which the [PHPCompatibility organisation](https://github.com/PHPCompatibility) maintains, in one go using Composer.


## What's included in this package ?

### Base ruleset

- [![PHPCompatibility Current Version](https://poser.pugx.org/phpcompatibility/php-compatibility/v/stable.png)](https://packagist.org/packages/phpcompatibility/php-compatibility) [PHPCompatibility](https://github.com/PHPCompatibility/PHPCompatibility) - External PHP_CodeSniffer standard to check your codebase for PHP cross-version compatibility.

### Framework/CMS specific rulesets

- [![PHPCompatibilityJoomla Current Version](https://poser.pugx.org/phpcompatibility/phpcompatibility-joomla/v/stable.png)](https://packagist.org/packages/PHPCompatibility/phpcompatibility-joomla) [PHPCompatibilityJoomla](https://github.com/PHPCompatibility/PHPCompatibilityJoomla) - PHPCompatibility ruleset specific for Joomla projects.
- [![PHPCompatibilityWP Current Version](https://poser.pugx.org/phpcompatibility/phpcompatibility-wp/v/stable.png)](https://packagist.org/packages/PHPCompatibility/phpcompatibility-wp) [PHPCompatibilityWP](https://github.com/PHPCompatibility/PHPCompatibilityWP) - PHPCompatibility ruleset specific for WordPress projects.

### Polyfill provider specific rulesets
- [![PHPCompatibilityPasswordCompat Current Version](https://poser.pugx.org/phpcompatibility/phpcompatibility-passwordcompat/v/stable.png)](https://packagist.org/packages/phpcompatibility/phpcompatibility-passwordcompat) [PHPCompatibilityPasswordCompat](https://github.com/PHPCompatibility/PHPCompatibilityPasswordCompat) - PHPCompatibility ruleset specific for projects which use @ircmaxell's [`password_compat`](https://github.com/ircmaxell/password_compat) polyfill library.
- [![PHPCompatibilityParagonie Current Version](https://poser.pugx.org/PHPCompatibility/phpcompatibility-paragonie/v/stable.png)](https://packagist.org/packages/phpcompatibility/phpcompatibility-paragonie) [PHPCompatibilityParagonie](https://github.com/PHPCompatibility/PHPCompatibilityParagonie) - PHPCompatibility rulesets for projects using either the Paragonie [`random_compat`](https://github.com/paragonie/random_compat) or the Paragonie [`sodium_compat`](https://github.com/paragonie/sodium_compat) polyfill library, or both.
- [![PHPCompatibilitySymfony Current Version](https://poser.pugx.org/PHPCompatibility/phpcompatibility-symfony/v/stable.png)](https://packagist.org/packages/phpcompatibility/phpcompatibility-symfony) [PHPCompatibilitySymfony](https://github.com/PHPCompatibility/PHPCompatibilitySymfony) - PHPCompatibility rulesets for projects using any of the [PHP polyfill libraries](https://github.com/symfony?utf8=?&q=polyfill) provided by the Symfony project.
    For more details about the available rulesets, please check out the [README of the PHPCompatibilitySymfony](https://github.com/PHPCompatibility/PHPCompatibilitySymfony/blob/master/README.md) repository.


## Requirements

* PHP 5.3+ for use with [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) 2.3.0+.
* PHP 5.4+ for use with [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) 3.0.2+.
* [Composer](https://getcomposer.org/)

Use the latest stable release of PHP_CodeSniffer for the best results.
The minimum _recommended_ version of PHP_CodeSniffer is version 2.6.0.


## Installation instructions

If you don't have a Composer plugin installed to manage the `installed_paths` setting for PHP_CodeSniffer, run the following from the command-line:
```bash
composer require --dev dealerdirect/phpcodesniffer-composer-installer:"^0.7" phpcompatibility/phpcompatibility-all:*
composer install
```

If you already have a Composer PHP_CodeSniffer plugin installed, run:
```bash
composer require --dev phpcompatibility/phpcompatibility-all:*
composer install
```

Next, run:
```bash
vendor/bin/phpcs -i
```
If all went well, you will now see that the `PHPCompatibility`, `PHPCompatibilityJoomla`, `PHPCompatibilityWP` and a number of polyfill related standards are installed for PHP_CodeSniffer.


## How to use

Now you can use any of the following commands to inspect your code:
```bash
./vendor/bin/phpcs -p . --standard=PHPCompatibility
./vendor/bin/phpcs -p . --standard=PHPCompatibilityJoomla
./vendor/bin/phpcs -p . --standard=PHPCompatibilityWP
./vendor/bin/phpcs -p . --standard=PHPCompatibilityPasswordCompat
./vendor/bin/phpcs -p . --standard=PHPCompatibilityParagonieRandomCompat
./vendor/bin/phpcs -p . --standard=PHPCompatibilityParagonieSodiumCompat
./vendor/bin/phpcs -p . --standard=PHPCompatibilitySymfonyPolyfillPHP54
./vendor/bin/phpcs -p . --standard=PHPCompatibilitySymfonyPolyfillPHP73
...etc...

# You can also combine the standards if your project uses several:
./vendor/bin/phpcs -p . --standard=PHPCompatibilityPasswordCompat,PHPCompatibilitySymfonyPolyfillPHP70,PHPCompatibilityWP
```

By default, you will only receive notifications about deprecated and/or removed PHP features.

To get the most out of the PHPCompatibility standards, you should specify a `testVersion` to check against. That will enable the checks for both deprecated/removed PHP features as well as the detection of code using new PHP features.

* You can run the checks for just one specific PHP version by adding `--runtime-set testVersion 5.5` to your command line command.
* You can also specify a range of PHP versions that your code needs to support. In this situation, compatibility issues that affect any of the PHP versions in that range will be reported: `--runtime-set testVersion 5.3-5.5`.
* Since PHPCompatibility 7.1.3, you can omit one part of the range if you want to support everything above or below a particular version, i.e. use `--runtime-set testVersion 7.0-` to run all the checks for PHP 7.0 and above.

For example:
```bash
# For a Joomla project which should be compatible with PHP 5.3 up to and including PHP 7.0:
./vendor/bin/phpcs -p . --standard=PHPCompatibilityJoomla --runtime-set testVersion 5.3-7.0

# For a project using both the Paragonie Sodium Compat polyfill as well as the Symfony PHP 7.1 polyfill and which should be compatible with PHP 5.4 and higher:
./vendor/bin/phpcs -p . --standard=PHPCompatibilityParagonieSodiumCompat,PHPCompatibilitySymfonyPolyfillPHP71 --runtime-set testVersion 5.4-
```

For more detailed information, see the README of the main [PHPCompatibility](https://github.com/PHPCompatibility/PHPCompatibility#sniffing-your-code-for-compatibility-with-specific-php-versions) standard.


### Testing PHP files only

By default PHP_CodeSniffer will analyse PHP, JavaScript and CSS files. As the PHPCompatibility sniffs only target PHP code, you can make the run slightly faster by telling PHP_CodeSniffer to only check PHP files, like so:
```bash
./vendor/bin/phpcs -p . --standard=PHPCompatibilitySymfonyPolyfillPHP56 --extensions=php --runtime-set testVersion 5.3-
```

## License

All code within the PHPCompatibility organisation is released under the GNU Lesser General Public License (LGPL).
For more information, visit https://www.gnu.org/copyleft/lesser.html


## Changelog

### 1.1.2 - 2021-02-16

- The recommended version of the [DealerDirect PHPCS Composer plugin] is now `^0.7.0`, which offers compatibility with Composer 2.0.
- The rulesets are now also tested against PHP 7.4 and 8.0.
    Note: full PHP 7.4 support is only available in combination with PHP_CodeSniffer >= 3.5.6.
    Note: runtime PHP 8.0 support is only available in combination with PHP_CodeSniffer >= 3.5.7, full support is expected in PHP_CodeSniffer 3.6.0.

### 1.1.1 - 2019-08-29

- The recommended version of the [DealerDirect PHPCS Composer plugin] is now `^0.5.0`.
- The rulesets are now also tested against PHP 7.3.
    Note: full PHP 7.3 support is only available in combination with PHP_CodeSniffer 2.9.2 or 3.3.1+ due to an incompatibility within PHP_CodeSniffer itself.

### 1.1.0 - 2018-10-07

- Added the new PHPCompatibilityPasswordCompat, PHPCompatibilityParagonie, PHPCompatibilitySymfony rulesets.

### 1.0.0 - 2018-07-17

Initial release containing the PHPCompatibility, PHPCompatibilityJoomla and PHPCompatibilityWP rulesets.

[DealerDirect PHPCS Composer plugin]: https://github.com/Dealerdirect/phpcodesniffer-composer-installer/
