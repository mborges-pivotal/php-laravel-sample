# php-laravel-sample
A sample code of PHP with Laravel 

## Deploy this app to localhost

```
$ git clone https://github.com/mborges-pivotal/php-laravel-sample.git
$ cd php-laravel-sample/
$ composer install
$ cp .env.example .env
$ php artisan key:generate
$ php artisan serve
```

Access to

- http://127.0.0.1:8000/

## Running on Cloud Foundry

* [PHP Buildpack Configuration](http://docs.cloudfoundry.org/buildpacks/php/gsg-php-config.html)

```
-> cat .bp-config/options.json
{
    "WEB_SERVER": "nginx",
    "WEBDIR": "public",
    "PHP_VERSION": "{PHP_72_LATEST}",
    "COMPOSER_VENDOR_DIR": "vendor"
}
```

We would like this sample able to exercise redis, postgres and twilio. The manifest below automatically binds the required services.

```
-> cat manifest.yml
---
applications:
- name: laravel
  memory: 128M
  instances: 1
  path: .
  services: []
  buildpack: php_buildpack
  env:
    BP_DEBUG: "False"
```
