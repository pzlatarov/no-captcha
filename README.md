No CAPTCHA reCAPTCHA [![Build Status](https://travis-ci.org/anhskohbo/no-captcha.svg?branch=master&style=flat-square)](https://travis-ci.org/anhskohbo/no-captcha)
==========

![recaptcha_anchor 2x](https://cloud.githubusercontent.com/assets/1529454/5291635/1c426412-7b88-11e4-8d16-46161a081ece.gif)

## Proxy support

This version was forked from anhskohbo's excellent implementation, but adds proxy support, in case the server is on a network that uses a proxy to access the Internet. 


## Installation

```
composer require pzlatarov/no-captcha
```

## Laravel 5

### Setup

Add ServiceProvider to the providers array in `app/config/app.php`.

```
Pzlatarov\NoCaptcha\NoCaptchaServiceProvider::class,
```

### Configuration

Add `NOCAPTCHA_SECRET` and `NOCAPTCHA_SITEKEY` in **.env** file:

```
NOCAPTCHA_SECRET=[secret-key]
NOCAPTCHA_SITEKEY=[site-key]
```

### Usage

##### Display reCAPTCHA

```php
{!! app('captcha')->display(); !!}
```

With custom attributes and language support:

```
{!! app('captcha')->display($attributes = [], $lang = null); !!}
```

##### Validation

Add `'g-recaptcha-response' => 'required|captcha'` to rules array.

```php

$validate = Validator::make(Input::all(), [
	'g-recaptcha-response' => 'required|captcha'
]);

```

## Without Laravel

Checkout example below:

```php
<?php

require_once "vendor/autoload.php";

$secret  = '';
$sitekey = '';
$captcha = new \Pzlatarov\NoCaptcha\NoCaptcha($secret, $sitekey);

if ( ! empty($_POST)) {
    var_dump($captcha->verifyResponse($_POST['g-recaptcha-response']));
    exit();
}

?>

<form action="?" method="POST">
    <?php echo $captcha->display(); ?>
    <button type="submit">Submit</button>
</form>

```

## Contribute

https://github.com/anhskohbo/no-captcha/pulls
