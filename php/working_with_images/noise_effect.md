# Noise effect

```php
function noise (&$image) {
    $imagex = imagesx($image);
    $imagey = imagesy($image);

    for ($x = 0; $x < $imagex; ++$x) {
        for ($y = 0; $y < $imagey; ++$y) {
            if (rand(0,1)) {
                $rgb = imagecolorat($image, $x, $y);
                $red = ($rgb >> 16) & 0xFF;
                $green = ($rgb >> 8) & 0xFF;
                $blue = $rgb & 0xFF;
                $modifier = rand(-20,20);
                $red += $modifier;
                $green += $modifier;
                $blue += $modifier;

                if ($red > 255) $red = 255;
                if ($green > 255) $green = 255;
                if ($blue > 255) $blue = 255;
                if ($red < 0) $red = 0;
                if ($green < 0) $green = 0;
                if ($blue < 0) $blue = 0;

                $newcol = imagecolorallocate($image, $red, $green, $blue);
                imagesetpixel($image, $x, $y, $newcol);
            }
        }
    }
}
```
