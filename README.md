# Base dockerized PHP project template

This is a dockerized PHP project template, currently using PHP 8 (RC).

**Provides:**

* PHP 8
* Composer 2
* ~~xdebug~~ (coming soon, when it is available for PHP 8)
* Testing
  * [PHPUnit](https://phpunit.de/)
* Static analysis
  * [phpstan](https://phpstan.org/)
* Code linting
  * [PHP Code Sniffer](https://github.com/squizlabs/PHP_CodeSniffer)
  
**Note:**
If using [Symfony](https://symfony.com/), remove PHPUnit first because Symfony uses [Symfony PHPUnit Bridge](https://symfony.com/doc/current/components/phpunit_bridge.html) instead.

## Requirements

* [Docker](https://www.docker.com/why-docker)

## Usage

### Install

#### Docker

* `docker-compose up --build`
* If you want to use xdebug, change the xdebug line in `docker-compose.yml` from `false` to `true` and run `docker-compose up --build` again.

#### PHP

* Composer is `docker/composer <command>`
  * PHPStan analysis: `docker/composer analyze`
  * PHPStan rebuild baseline: `docker/composer analyse-baseline`
  * Code Sniffer lint: `docker/composer lint`
  * Code Sniffer code-fix: `docker/composer lint-fix`
* Anything else that would normally be run using PHP will probably be `docker/app <command`
  * Example: `docker/app php --version`
  * PHPUnit: `docker/app vendor/bin/phpunit`
