# PHPCompatibilityAll

[![License](https://img.shields.io/github/license/PHPCompatibility/PHPCompatibilityAll?color=00a7a7)](https://github.com/PHPCompatibility/PHPCompatibilityAll/blob/master/LICENSE)
[![Build Status](https://github.com/PHPCompatibility/PHPCompatibilityAll/actions/workflows/validate.yml/badge.svg?branch=master)](https://github.com/PHPCompatibility/PHPCompatibilityAll/actions/workflows/validate.yml)

Convenience package to install all the external PHP_CodeSniffer rulesets which the [PHPCompatibility organisation](https://github.com/PHPCompatibility) maintains, in one go using Composer.


## Funding

**This project needs funding.**

The project team has spend thousands of hours creating and maintaining the PHPCompatibility packages. This is unsustainable without funding.

If you use PHPCompatibility, please fund this work by setting up a monthly contribution to the [PHP_CodeSniffer Open Collective].


## What's included in this package ?

### Base ruleset

* [![PHPCompatibility Current Version](https://img.shields.io/packagist/v/phpcompatibility/php-compatibility?label=stable)](https://packagist.org/packages/phpcompatibility/php-compatibility) [PHPCompatibility] - External PHP_CodeSniffer standard to check your codebase for PHP cross-version compatibility.

### Framework/CMS specific rulesets

* [![PHPCompatibilityJoomla Current Version](https://img.shields.io/packagist/v/phpcompatibility/phpcompatibility-joomla?label=stable)](https://packagist.org/packages/PHPCompatibility/phpcompatibility-joomla) [PHPCompatibilityJoomla] - PHPCompatibility ruleset specific for Joomla projects.
* [![PHPCompatibilityWP Current Version](https://img.shields.io/packagist/v/phpcompatibility/phpcompatibility-wp?label=stable)](https://packagist.org/packages/PHPCompatibility/phpcompatibility-wp) [PHPCompatibilityWP] - PHPCompatibility ruleset specific for WordPress projects.

### Polyfill provider specific rulesets
* [![PHPCompatibilityPasswordCompat Current Version](https://img.shields.io/packagist/v/phpcompatibility/phpcompatibility-passwordcompat?label=stable)](https://packagist.org/packages/phpcompatibility/phpcompatibility-passwordcompat) [PHPCompatibilityPasswordCompat] - PHPCompatibility ruleset specific for projects which use @ircmaxell's [`password_compat`] polyfill library.
* [![PHPCompatibilityParagonie Current Version](https://img.shields.io/packagist/v/phpcompatibility/phpcompatibility-paragonie?label=stable)](https://packagist.org/packages/phpcompatibility/phpcompatibility-paragonie) [PHPCompatibilityParagonie] - PHPCompatibility rulesets for projects using either the Paragonie [`random_compat`] or the Paragonie [`sodium_compat`] polyfill library, or both.
* [![PHPCompatibilitySymfony Current Version](https://img.shields.io/packagist/v/phpcompatibility/phpcompatibility-symfony?label=stable)](https://packagist.org/packages/phpcompatibility/phpcompatibility-symfony) [PHPCompatibilitySymfony] - PHPCompatibility rulesets for projects using any of the [PHP polyfill libraries] provided by the Symfony project.
    For more details about the available rulesets, please check out the [README of the PHPCompatibilitySymfony][PHPCompatibilitySymfony-readme] repository.


## Requirements

* PHP > 5.4
* [PHP_CodeSniffer] > 3.13.3.
    Use the latest stable release of PHP_CodeSniffer for the best results.
* [Composer]


## Installation instructions

The only supported installation method is via [Composer].

[Composer] will automatically install the project dependencies and register the external rulesets with PHP_CodeSniffer using the [Composer PHPCS plugin].

Run the following from the root of your project:
```bash
composer config allow-plugins.dealerdirect/phpcodesniffer-composer-installer true
composer require --dev phpcompatibility/phpcompatibility-all:"^2.0@dev"
```

Next, run:
```bash
vendor/bin/phpcs -i
```
If all went well, you will now see that the `PHPCompatibility`, `PHPCompatibilityJoomla`, `PHPCompatibilityWP` and a number of polyfill related standards are installed for PHP_CodeSniffer.


## Upgrade instructions

To upgrade this package, run the following command:
```bash
composer update --dev phpcompatibility/phpcompatibility-all --with-dependencies
```

> [!TIP]
> If you have a _root_ requirement in your project for one of the packages used by this project, you may need to update with `--with-all-dependencies` instead.


## How to use

You can now use any of the following commands to inspect your code:
```bash
vendor/bin/phpcs -p . --standard=PHPCompatibility
vendor/bin/phpcs -p . --standard=PHPCompatibilityJoomla
vendor/bin/phpcs -p . --standard=PHPCompatibilityWP
vendor/bin/phpcs -p . --standard=PHPCompatibilityPasswordCompat
vendor/bin/phpcs -p . --standard=PHPCompatibilityParagonieRandomCompat
vendor/bin/phpcs -p . --standard=PHPCompatibilityParagonieSodiumCompat
vendor/bin/phpcs -p . --standard=PHPCompatibilitySymfonyPolyfillPHP54
vendor/bin/phpcs -p . --standard=PHPCompatibilitySymfonyPolyfillPHP73
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
vendor/bin/phpcs -p . --standard=PHPCompatibilityJoomla --runtime-set testVersion 5.3-7.0

# For a project using both the Paragonie Sodium Compat polyfill, as well as the Symfony
# PHP 7.1 polyfill and which should be compatible with PHP 5.4 and higher:
vendor/bin/phpcs -p . --standard=PHPCompatibilityParagonieSodiumCompat,PHPCompatibilitySymfonyPolyfillPHP71 --runtime-set testVersion 5.4-
```

For more detailed information, see the README of the main [PHPCompatibility][PHPCompatibility-testVersion] standard.


### Testing PHP files only

By default PHP_CodeSniffer will analyse PHP, JavaScript and CSS files. As the PHPCompatibility sniffs only target PHP code, you can make the run slightly faster by telling PHP_CodeSniffer to only check PHP files, like so:
```bash
vendor/bin/phpcs -p . --standard=PHPCompatibilitySymfonyPolyfillPHP56 --extensions=php --runtime-set testVersion 5.3-
```

## License

All code within the PHPCompatibility organisation is released under the GNU Lesser General Public License (LGPL).
For more information, visit <https://www.gnu.org/licenses/lgpl-3.0.html>.


[Composer]:                        https://getcomposer.org/
[Composer PHPCS plugin]:           https://github.com/PHPCSStandards/composer-installer/
[PHP_CodeSniffer]:                 https://github.com/PHPCSStandards/PHP_CodeSniffer
[PHP_CodeSniffer Open Collective]: https://opencollective.com/php_codesniffer
[PHPCompatibility]:                https://github.com/PHPCompatibility/PHPCompatibility
[PHPCompatibility-testVersion]:    https://github.com/PHPCompatibility/PHPCompatibility#sniffing-your-code-for-compatibility-with-specific-php-versions
[PHPCompatibilityParagonie]:       https://github.com/PHPCompatibility/PHPCompatibilityParagonie
[PHPCompatibilityPasswordCompat]:  https://github.com/PHPCompatibility/PHPCompatibilityPasswordCompat
[PHPCompatibilitySymfony]:         https://github.com/PHPCompatibility/PHPCompatibilitySymfony
[PHPCompatibilityJoomla]:          https://github.com/PHPCompatibility/PHPCompatibilityJoomla
[PHPCompatibilityWP]:              https://github.com/PHPCompatibility/PHPCompatibilityWP
[`password_compat`]:               https://github.com/ircmaxell/password_compat
[`random_compat`]:                 https://github.com/paragonie/random_compat
[`sodium_compat`]:                 https://github.com/paragonie/sodium_compat
[PHP polyfill libraries]:          https://github.com/symfony?utf8=?&q=polyfill
[PHPCompatibilitySymfony-readme]:  https://github.com/PHPCompatibility/PHPCompatibilitySymfony/blob/master/README.md
