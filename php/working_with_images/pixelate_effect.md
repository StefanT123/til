# Pixelate effect

```php
function pixelate(&$image) {
    $imagex = imagesx($image);
    $imagey = imagesy($image);
    $blocksize = 12;

    for ($x = 0; $x < $imagex; $x += $blocksize) {
        for ($y = 0; $y < $imagey; $y += $blocksize) {
            $rgb = imagecolorat($image, $x, $y);
            imagefilledrectangle($image, $x, $y, $x + $blocksize - 1, $y + $blocksize - 1, $rgb);
        }
    }
}
```

---

More complicated and better way
```php
function pixelate(&$image) {
    $imagex = imagesx($image);
    $imagey = imagesy($image);
    $blocksize = 12;

    for ($x = 0; $x < $imagex; $x += $blocksize) {
        for ($y = 0; $y < $imagey; $y += $blocksize) {
            // get the pixel colour at the top-left of the square
            $thiscol = imagecolorat($image, $x, $y);

            // set the new red, green, and blue values to 0
            $newr = 0;
            $newg = 0;
            $newb = 0;

            // create an empty array for the colours
            $colours = array();

            // cycle through each pixel in the block
            for ($k = $x; $k < $x + $blocksize; ++$k) {
                for ($l = $y; $l < $y + $blocksize; ++$l) {
                    // if we are outside the valid bounds of the image, use a safe colour
                    if ($k < 0) { $colours[] = $thiscol; continue; }
                    if ($k >= $imagex) { $colours[] = $thiscol; continue; }
                    if ($l < 0) { $colours[] = $thiscol; continue; }
                    if ($l >= $imagey) { $colours[] = $thiscol; continue; }

                    // if not outside the image bounds, get the colour at this pixel
                    $colours[] = imagecolorat($image, $k, $l);
                }
            }

            // cycle through all the colours we can use for sampling
            foreach($colours as $colour) {
                // add their red, green, and blue values to our master numbers
                $newr += ($colour >> 16) & 0xFF;
                $newg += ($colour >> 8) & 0xFF;
                $newb += $colour & 0xFF;
            }

            // now divide the master numbers by the number of valid samples to get an average
            $numelements = count($colours);
            $newr /= $numelements;
            $newg /= $numelements;
            $newb /= $numelements;

            // and use the new numbers as our colour
            $newcol = imagecolorallocate($image, $newr, $newg, $newb);
            imagefilledrectangle($image, $x, $y, $x + $blocksize - 1, $y + $blocksize - 1, $newcol);
        }
    }
}
```
