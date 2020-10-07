# Base dockerized PHP project template

This is a dockerized PHP project template, currently using PHP 8 (RC).

## Requirements

* Docker

## Usage

### Install

#### Docker

* `docker-compose up --build`
* If you want to use xdebug, change the xdebug line in `docker-compose.yml` from `false` to `true` and run `docker-compose up --build` again.

#### PHP

* Composer is `docker/composer <command>`
* Anything else that would normally be run using PHP will probably be `docker/app <command`
  * Example: `docker/app php --version`
