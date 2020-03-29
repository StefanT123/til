# Create an image

```php
header('Content-Type: image/png');
$image = imagecreate(400,300); //create image
$gold = imagecolorallocate($image, 255, 240, 00); //set the background color of the created image
imagepng($image); // output the image as png
imagedestroy($image); // free space at the end
```
