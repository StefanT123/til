# Duotone image

```php
function duotone (&$image, $rplus, $gplus, $bplus) {
    $imagex = imagesx($image);
    $imagey = imagesy($image);

    for ($x = 0; $x <$imagex; ++$x) {
        for ($y = 0; $y <$imagey; ++$y) {
            $rgb = imagecolorat($image, $x, $y);
            $red = ($rgb >> 16) & 0xFF;
            $green = ($rgb >> 8) & 0xFF;
            $blue = $rgb & 0xFF;
            $red = (int)(($red+$green+$blue)/3);
            $green = $red + $gplus;
            $blue = $red + $bplus;
            $red += $rplus;

            if ($red > 255) $red = 255;
            if ($green > 255) $green = 255;
            if ($blue > 255) $blue = 255;
            if ($red < 0) $red = 0;
            if ($green < 0) $green = 0;
            if ($blue < 0) $blue = 0;

            $newcol = imagecolorallocate ($image, $red,$green,$blue);
            imagesetpixel ($image, $x, $y, $newcol);
        }
    }
}
```
