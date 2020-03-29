# Screen effect

```php
function screen(&$image) {
    $imagex = imagesx($image);
    $imagey = imagesy($image);
    GLOBAL $black;

    for($x = 1; $x <= $imagex; $x += 2) {
        imageline($image, $x, 0, $x, $imagey, $black);
    }

    for($y = 1; $y <= $imagey; $y += 2) {
        imageline($image, 0, $y, $imagex, $y, $black);
    }
}
```
