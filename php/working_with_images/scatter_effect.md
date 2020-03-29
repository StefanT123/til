# Scatter effect

```php
function scatter(&$image) {
    $imagex = imagesx($image);
    $imagey = imagesy($image);

    for ($x = 0; $x < $imagex; ++$x) {
        for ($y = 0; $y < $imagey; ++$y) {
            $distx = rand(-4, 4);
            $disty = rand(-4, 4);

            if ($x + $distx >= $imagex) continue;
            if ($x + $distx < 0) continue;
            if ($y + $disty >= $imagey) continue;
            if ($y + $disty < 0) continue;

            $oldcol = imagecolorat($image, $x, $y);
            $newcol = imagecolorat($image, $x + $distx, $y + $disty);
            imagesetpixel($image, $x, $y, $newcol);
            imagesetpixel($image, $x + $distx, $y + $disty, $oldcol);
        }
    }
}
```
