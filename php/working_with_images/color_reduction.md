# Color reduction

```php
set_time_limit(0);
$image = imagecreatefrompng("space.png");
imagetruecolortopalette($image, true, 64);
header("image/png");
imagepng($image);
imagedestroy($image);
```
