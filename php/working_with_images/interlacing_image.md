# Interlacing image

```php
function interlace (&$image) {
    $imagex = imagesx($image);
    $imagey = imagesy($image);
    GLOBAL $black;

    for ($y = 1; $y < $imagey; $y += 2) {
        imageline($image, 0, $y, $imagex, $y, $black);
    }
}

$image = imagecreatefrompng("space.png");
$black = imagecolorallocate($image, 0, 0, 0);
interlace($image);

header("image/png");
imagepng($image);
imagedestroy($image);
```
