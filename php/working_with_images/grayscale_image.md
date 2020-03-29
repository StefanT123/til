# Grayscale image

We can use the >> operator in combination with the & operator to get red and green. Our red 192, green 193, blue 194 colour was 110000001100000111000010 in binary. To get the blue out of that, as you know, we can just & the number with 255 to get the last eight bits. To get green, we need to shift the whole number eight places to the right so that the blue number is cut off, then & the result with 255. To get red, we need to shift the number sixteen places to the right so that both the green and blue numbers are cut off, then again & the result with 255
```php
function greyscale (&$image) {
    $imagex = imagesx($image);
    $imagey = imagesy($image);

    for ($x = 0; $x <$imagex; ++$x) {
        for ($y = 0; $y <$imagey; ++$y) {
            $rgb = imagecolorat($image, $x, $y); // grab the color value for the current pixel
            $red = ($rgb >> 16) & 255;
            $green = ($rgb >> 8) & 255;
            $blue = $rgb & 255;
            $grey = (int) (($red+$green+$blue) / 3);
            $newcol = imagecolorallocate($image, $grey, $grey, $grey);
            imagesetpixel($image, $x, $y, $newcol);
        }
    }
}
```
