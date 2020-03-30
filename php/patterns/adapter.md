# Adapter

Adapter allows us to translate or wrap one interface for use with another

It's used when the interfaces don't match (most likely when we are using a package)
```php
interface BookInterface
{
    public function open();
    public function turnPage();
}

class Book implements BookInterface
{
    public function open()
    {
        var_dump('opening the paper book');
    }

    public function turnPage()
    {
        var_dump('turning the page of the paper book');
    }
}

interface eReaderInterface
{
    public function turnOn();
    public function pressNextButton();
}

class Kindle implements eReaderInterface
{
    public function turnOn()
    {
        var_dump('turn the kindle on');
    }

    public function pressNextButton()
    {
        var_dump('press the next button on the kindle');
    }
}

class Nook implements eReaderInterface
{
    public function turnOn()
    {
        var_dump('turn the Nook on');
    }

    public function pressNextButton()
    {
        var_dump('press the next button on the Nook');
    }
}

class eReaderAdapter implements BookInterface
{
    protected $reader;

    public function __construct(eReaderInterface $reader)
    {
        $this->reader = $reader;
    }

    public function open()
    {
        return $this->reader->turnOn();
    }

    public function turnPage()
    {
        return $this->reader->pressNextButton();
    }
}

class Person
{
    public function read(BookInterface $book)
    {
        $book->open();
        $book->turnPage();
    }
}

(new Person)->read(new Book);
(new Person)->read(new eReaderAdapter(new Kindle));
(new Person)->read(new eReaderAdapter(new Nook));
```
