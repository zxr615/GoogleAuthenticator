Google Authenticator PHP 
==============================

* Copyright (c) 2012-2016, [http://www.phpgangsta.de](http://www.phpgangsta.de)
* Author: Michael Kliewe, [@PHPGangsta](http://twitter.com/PHPGangsta) and [contributors](https://github.com/PHPGangsta/GoogleAuthenticator/graphs/contributors)
* Licensed under the BSD License.

This PHP class can be used to interact with the Google Authenticator mobile app for 2-factor-authentication. This class
can generate secrets, generate codes, validate codes and present a QR-Code for scanning the secret. It implements TOTP 
according to [RFC6238](https://tools.ietf.org/html/rfc6238)

For a secure installation you have to make sure that used codes cannot be reused (replay-attack). You also need to
limit the number of verifications, to fight against brute-force attacks. For example you could limit the amount of
verifications to 10 tries within 10 minutes for one IP address (or IPv6 block). It depends on your environment.

Usage:
------

See following example:

`composer require "fanwei/googleauthenticator:1.0.*"`

```php
<?php

use Fanwei\GoogleAuthenticator\GoogleAuthenticator;

$ga = new GoogleAuthenticator();
// 创建
$secret = $ga->createSecret();
// 获取 code
$code = $ga->getCode($secret);
// 验证 code 
$res = $ga->verifyCode($secret, $code);
// 获取二维码字符串
$qrcodeString = $ga->getQrcodeString($secret, 'GoogleAuthenticator');
```
Running the script provides the following output:
```
Secret is：WLRAQ5KGUC7YCR75
Code is：577963
res：true
qrcodeString：otpauth://totp/GoogleAuthenticator?secret=WLRAQ5KGUC7YCR75
```
