# Creating temporary file

It will create a temporary file on the system, fopen() it for you, and send back the file handle as its return value (file is deleted as soon as we fclose() the file)
```php
tmpfile();
sys_get_temp_dir() // If we want to know where these temp files are being saved
```
