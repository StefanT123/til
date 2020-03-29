# Writing text in an image

```php
$image = imagecreate(400, 300);
$blue = imagecolorallocate($image, 0, 0, 255);
$white = ImageColorAllocate($image, 255,255,255);

if (! isset($_GET['size'])) $_GET['size'] = 44;
if (! isset($_GET['text'])) $_GET['text'] = "Hello, world!";

imagettftext($image, $_GET['size'], 15, 50, 200, $white, "ARIAL", $_GET['text']);
header("content-type: image/png");
imagepng($image);
imagedestroy($image);
```
