# Blur effect

```php
function blur (&$image) {
    $imagex = imagesx($image);
    $imagey = imagesy($image);
    $dist = 1;

    for ($x = 0; $x < $imagex; ++$x) {
        for ($y = 0; $y < $imagey; ++$y) {
            $newr = 0;
            $newg = 0;
            $newb = 0;

            $colours = array();
            $thiscol = imagecolorat($image, $x, $y);

            for ($k = $x - $dist; $k <= $x + $dist; ++$k) {
                for ($l = $y - $dist; $l <= $y + $dist; ++$l) {
                    if ($k < 0) { $colours[] = $thiscol; continue; }
                    if ($k >= $imagex) { $colours[] = $thiscol; continue; }
                    if ($l < 0) { $colours[] = $thiscol; continue; }
                    if ($l >= $imagey) { $colours[] = $thiscol; continue; }
                    $colours[] = imagecolorat($image, $k, $l);
                }
            }

            foreach($colours as $colour) {
                $newr += ($colour >> 16) & 0xFF;
                $newg += ($colour >> 8) & 0xFF;
                $newb += $colour & 0xFF;
            }

            $numelements = count($colours);
            $newr /= $numelements;
            $newg /= $numelements;
            $newb /= $numelements;

            $newcol = imagecolorallocate($image, $newr, $newg, $newb);
            imagesetpixel($image, $x, $y, $newcol);
        }
    }
}
```
