# Changelog for PHPCompatibilityAll

All notable changes to this project will be documented in this file.

This projects adheres to [Semantic Versioning](https://semver.org/) and [Keep a CHANGELOG](https://keepachangelog.com/).

## [2.0.0-alpha1] - 2025-10-22

* Composer: All PHPCompatibility dependencies have been updated to the recently released PHPCompatibility 10.0.0-alpha1 based versions.
    Note: in select cases, this means that custom `<exclude>` rules in a project's `[.]phpcs.xml[.dist]` configuration file may needs to be updated.
    Along the same lines, selective `// phpcs:ignore` comments used inline may need to be updated with the new sniff code(s).
    For full information on these kind of changes, please refer to the [Upgrade guide for PHPCompatibility 10.0.0][phpcompat-wiki-upgrade-10].
* The [Composer PHPCS plugin] will now be installed automatically to register PHPCompatibility and other external standards with PHP_CodeSniffer.
    If you have a `require-dev` in place for this plugin in your own `composer.json`, it is strongly recommended to remove this to prevent conflicting version constraints.
    If you previously used another Composer plugin, manually set the `installed_paths` configuration, or set the `installed_paths` in your `[.]phpcs.xml[.dist]` configuration file, it is recommended you remove this in favour of letting the [Composer PHPCS plugin] handle this.
* Support for PHP 5.3 has been dropped. The new minimum supported PHP version is 5.4.
* Support for PHP_CodeSniffer 4.0 has been added.
* Support for PHP_CodeSniffer < 3.13.3 has been dropped.

[phpcompat-wiki-upgrade-10]: https://github.com/PHPCompatibility/PHPCompatibility/wiki/Upgrading-to-PHPCompatibility-10.0

## [1.1.5] - 2025-10-18

* General housekeeping and maintenance.

## [1.1.4] - 2025-01-16

This is a maintenance release.

* The recommended version of the [Composer PHPCS plugin] is now `^1.0.0`.
* README: Fixed some broken badges.
* General housekeeping and maintenance. Including a contribution by [@fredden].

## [1.1.3] - 2022-10-30

* README: Updated the installation instructions for [compatibility with Composer >= 2.2][composer22announce].
* Composer: The package will now identify itself as a static analysis tool. Thanks [@GaryJones]!
* Other housekeeping and minor documentation updates.

[composer22announce]: https://blog.packagist.com/composer-2-2/#more-secure-plugin-execution

## [1.1.2] - 2021-02-16

* The recommended version of the [Composer PHPCS plugin] is now `^0.7.0`, which offers compatibility with Composer 2.0.
* The rulesets are now also tested against PHP 7.4 and 8.0.
    Note: full PHP 7.4 support is only available in combination with PHP_CodeSniffer >= 3.5.6.
    Note: runtime PHP 8.0 support is only available in combination with PHP_CodeSniffer >= 3.5.7, full support is expected in PHP_CodeSniffer 3.6.0.

## [1.1.1] - 2019-08-29

* The recommended version of the [Composer PHPCS plugin] is now `^0.5.0`.
* The rulesets are now also tested against PHP 7.3.
    Note: full PHP 7.3 support is only available in combination with PHP_CodeSniffer 2.9.2 or 3.3.1+ due to an incompatibility within PHP_CodeSniffer itself.

## [1.1.0] - 2018-10-07

* Added the new PHPCompatibilityPasswordCompat, PHPCompatibilityParagonie, PHPCompatibilitySymfony rulesets.

## 1.0.0 - 2018-07-17

Initial release containing the PHPCompatibility, PHPCompatibilityJoomla and PHPCompatibilityWP rulesets.

[Composer PHPCS plugin]: https://github.com/PHPCSStandards/composer-installer/

[2.0.0-alpha1]: https://github.com/PHPCompatibility/PHPCompatibilityAll/compare/1.1.5...2.0.0-alpha1
[1.1.5]:        https://github.com/PHPCompatibility/PHPCompatibilityAll/compare/1.1.4...1.1.5
[1.1.4]:        https://github.com/PHPCompatibility/PHPCompatibilityAll/compare/1.1.3...1.1.4
[1.1.3]:        https://github.com/PHPCompatibility/PHPCompatibilityAll/compare/1.1.2...1.1.3
[1.1.2]:        https://github.com/PHPCompatibility/PHPCompatibilityAll/compare/1.1.1...1.1.2
[1.1.1]:        https://github.com/PHPCompatibility/PHPCompatibilityAll/compare/1.1.0...1.1.1
[1.1.0]:        https://github.com/PHPCompatibility/PHPCompatibilityAll/compare/1.0.0...1.1.0

[@fredden]:   https://github.com/fredden
[@GaryJones]: https://github.com/GaryJones
