# php-laravel-hello-world
A sample code of PHP with Laravel from [niwasawa/php-laravel-hello-world](https://github.com/niwasawa/php-laravel-hello-world). We didn't fork because we'll modify to include additional tests to support postgres, redis and twilio. We'll also include concourse pipeline and create a docker image.

## Deploy this app to localhost

```
$ git clone https://github.com/niwasawa/php-laravel-hello-world.git
$ cd php-laravel-hello-world/
$ composer install
$ php artisan serve
```

Access to

- http://127.0.0.1:8000/
- http://127.0.0.1:8000/hello/
- http://127.0.0.1:8000/world/

## Running on Cloud Foundry

* [PHP Buildpack Configuration](http://docs.cloudfoundry.org/buildpacks/php/gsg-php-config.html)

```
-> cat .bp-config/options.json
{
    "WEB_SERVER": "nginx",
    "WEBDIR": "public",
    "PHP_VERSION": "PHP_70_LATEST",
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
  services: [ postgresql, redis ]
  buildpack: php_buildpack
  env:
    BP_DEBUG: "False"
```
