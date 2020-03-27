# Too many arguments in a method

When a function accepts 4 args or more and we have many conditions that might be an indication that we are missing a class:
```php
function compress($files, $fileType, $destination, $compressor)
{
    if ($fileType == 'css') } {
        // compress css
    }

    if ($fileType == 'js') } {
        if ($compressor) {
            $compressor($files);
        }
    }
}
```

Instead we can extract a class:
```php
interface CompressionStrategy
{
    public function fire();
}

class JavascriptDriver implements CommpressionStrategy
{
    protected $files;

    public function __construct($files)
    {
        $this->files = $files;
    }

    public function fire()
    {
        // compressing js files
    }
}

function compress(CompressionStrategy $strategy, $destination)
{
    $compressed = $strategy->fire();
}

compress(new JavascriptStrategy($files), $destination);
```
