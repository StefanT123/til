# Fitting a text in a box

Fitting text into an exact space is a complex art, particularly when you rotate the text too. PHP makes the job easier with the function `imagettfbbox()`, which will return an array containing the co-ordinates of a bounding box around the text – literally how big it is in each of its dimensions. The complication here is that it is tricky to get the co-ordinate system right, as the numbers returned seem easier to use than they actually are.
```php
if (! isset($_GET['size'])) $_GET['size'] = 44;
if (! isset($_GET['text'])) $_GET['text'] = "Hello, world!";

$size = imagettfbbox($_GET['size'], 0, "ARIAL", $_GET['text']);
$xsize = abs($size[0]) + abs($size[2]);
$ysize = abs($size[5]) + abs($size[1]);

$image = imagecreate($xsize, $ysize);
$blue = imagecolorallocate($image, 0, 0, 255);
$white = ImageColorAllocate($image, 255,255,255);
imagettftext($image, $_GET['size'], 0, abs($size[0]), abs($size[5]), $white, "ARIAL", $_GET['text']);

header("content-type: image/png");
imagepng($image);
imagedestroy($image);
```
