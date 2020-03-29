# Images functions

Header() outputs a HTTP header of your choice, and in this situation we will be sending the content-type header, which tells web browsers what kind of content they can expect through the connection. Popular content types include text/plain for plain text documents, `text/html` for most web pages, and `image/*`, where the * is PNG, JPEG, GIF, or other picture formats

As image memory is not automatically cleaned up for you, you need to be especially careful to call `image_destroy()` on all your image resources once you are finished with them

**Warning! You must never forget to call imagedestroy() otherwise your web server will slowly chew up more and more system resources until your server all but locks up. Always keep your scripts in order - don't forget to clean up after yourself!**
```php
imagecreate(x_size, y_size) // creates an image, returns false if it fails
imagedestroy(im) // frees up the memory assigned to the image

imagepng(im, to, quality, filters) // output the picture in PNG
imagejpeg(im, to, quality) // ouptputs the picture in JPEG

imagecolorallocate($image, 255, 240, 00); //set the background color of the created image
imagefilledrectangle(im, x1, y1, x2, y2, col) // takes six parameters in total, which are, in order: an image resource to draw on, the top-left X coordinate, the top-left Y coordinate, the bottom-right X coordinate, the bottom-right Y coordinate, and a colour to use
imagerectangle(im, x1, y1, x2, y2, col) // draws only the outline of the rectangle
imagecreatetruecolor(x_size, y_size) // same as imagecreate() (The differences between the two are that imagecreatetruecolor() returns an image with a true-colour palette, whereas imagecreate() only lets you use 256 colours at once)
imagefilledellipse(im, cx, cy, w, h, color) // create ellipsis
imagefilledarc(im, cx, cy, w, h, s, e, col, style) // create arc
imagefilledarc($image, 200, 150, 200, 200, 345, 15, $green, IMG_ARC_CHORD | IMG_ARC_NOFILL);
imagefilledarc($image, 200, 150, 200, 200, 345, 15, $green, IMG_ARC_EDGED | IMG_ARC_NOFILL);
imagefilledpolygon(im, points, num_pos, col) // create polygon
imagecolortransparent(im, col) // setting transparency of the image
imagecopyresized(dst_im, src_im, dst_x, dst_y, src_x, src_y, dst_w, dst_h, src_w, src_h) // resizing image (low-quality)
imagecopyresampled(dst_im, src_im, dst_x, dst_y, src_x, src_y, dst_w, dst_h, src_w, src_h) // resizing image (high-quality - more loading time)
imagefilter(im, filtertype, arg1, arg2, arg3, arg4) // special effects for image
imagettftext(); // which takes eight parameters in total: the image resource to draw on, font size to use, angle to draw at, X co-ordinate, Y co-ordinate, color, font file, and the text to write.

$info = getimagesize("button.png");
image_type_to_mime_type($info[2]); // get MIME type of the image

imagedestroy($image); // free space at the end
```
