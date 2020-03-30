# Single responsibility principle

**A CLASS SHOULD HAVE ONE, AND ONLY ONE, REASON TO CHANGE**

A class should have only a single responsibility. Only one potential change in the software’s specification should be able to affect the specification of the class

### Real world example
![](images/SRP.jpeg)

### Code

**Without SRP**
```php
class SalesReporter
{
    protected $repo;

    public function __construct(SalesRepository $repo)
    {
        $this->repo = $repo;
    }

    public function between($startDate, $endDate)
    {
        // preform auth
        if (!Auth::check()) throw new Exception('Authentication required for reporting');
        // why would SalesReporter have interest in auth user?!
        // IT DOESN'T BELONG HERE
        // EXTRACT it to a controller

        // get sales from db
        $sales = $this->queryDBForSalesBetween($startDate, $endDate);

        // return results
        return $this->format($sales);
    }

    public function queryDBForSalesBetween($startDate, $endDate)
    {
        // this class don't need to know how we fetch some data from the database
        // we should extract this logic into his own class and then pass it through the constructor
        return DB::table('sales')->whereBetween('created_at', [$startDate, $endDate])->sum('charge');
    }

    public function format($sales)
    {
        // if we would to change the format of the output we would have to make a change in this class
        // this class shouldn't have the respomsability for the html output
        // if we don't know the desired output format we should extract this (into interface, so we could have the desired output without changing anything)
        return "<h2>Sales: $sales</h2>";
    }
}
```

**With SRP**
```php
class SalesReporter
{
    protected $repo;

    public function __construct(SalesRepository $repo)
    {
        $this->repo = $repo;
    }

    public function between($startDate, $endDate, SalesOutputInteface $formatter)
    {
        // logic from the SalesRepository controller
        $sales = $this->repo->between($startDate, $endDate);

        // because we know for certain that every class that implements SalesOutputInterface will have the output function
        // we call that function
        // we can then pass HtmlOutput into the between as 3rd argument, or any class that implements SalesOutputInteface!!
        return $formatter->output($sales);
    }
}

class SalesRepository
{
    public function between($startDate, $endDate)
    {
        return DB::table('sales')->whereBetween('created_at', [$startDate, $endDate])->sum('charge');
    }
}

interface SalesOutputInteface
{
    // we tell every class that implements this interface that it must have output function
    public function output($sales);
}

class HtmlOutput implements SalesOutputInteface
{
    public function output($sales)
    {
        return "<h2>Sales: $sales</h2>";
    }
}

class ViewController extends Controller
{
    public function index()
    {
        $report = new SalesReporter(new SalesRepository);

        $begin = Carbon\Carbon::now()->subDays(10);
        $end = Carbon\Carbon::now();

        // we can pass HtmlOutput or any other output that implements SalesOutputInteface interface
        return $report->between($begin, $end, new HtmlOutput);
    }
}
```
