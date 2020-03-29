# CURL

The `curl_init()` function returns a Curl instance for us to use in later functions, and you should always store it for later. It has just one optional parameter: if you pass a string into `curl_init()`, it will automatically use that string as the URL to work with. In the script below, we use `curl_setopt()` to do that for clarity, but it is all the same

`curl_setopt()` takes three parameters, which are the Curl instance to use, a constant value for the setting you want to change, and the value you want to use for that setting. There are a huge number of constants you can use for settings, and many of these are listed shortly. In the example we use `CURLOPT_URL`, which is used to set the URL for Curl to work with, and so the working URL is set to the third parameter

Calling `curl_exec()` means, "We're finished setting our options, go ahead and do it", and you need to pass precisely one parameter: the Curl resource to use. The return value of `curl_exec()` is true/false by default

The final function, `curl_close()`, takes a Curl resource as its only parameter, closes the Curl session, then frees up the associated memory
```php
$curl = curl_init();
curl_setopt($curl, CURLOPT_URL, "http://localhost/posttest.php");
curl_setopt($curl, CURLOPT_POST, 1);
curl_setopt($curl, CURLOPT_POSTFIELDS, "Hello=World&Foo=Bar&Baz=Wombat");

curl_exec ($curl);
curl_close ($curl);
```
