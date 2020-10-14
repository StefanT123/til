# Stacks

Array
```js
class Stack {
  constructor() {
    this.stack = []
  }

  // Inserts the element into the top of the stack
  push(element) {
    this.stack.push(element)
  }

  // Removes the element from the top of the stack and return that element
  pop() {
    if (this.isEmpty()) return 'Stack is empty!'
    return this.stack.pop()
  }

  // Return which element is on top of the stack
  peek() {
    if (this.isEmpty()) return 'Stack is empty'
    return this.stack[this.stack.length - 1]
  }

  // helper method
  isEmpty() {
    return !this.stack.length
  }
}
```

---

Stack in O(1) (constant) time and space complexity
```php
class MinStack {
    protected $stack;
    protected $min;

    /**
     * initialize your data structure here.
     */
    function __construct() {
        $this->stack = [];
    }

    /**
     * @param Integer $x
     * @return NULL
     */
    function push($x) {
        if (count($this->stack) < 1) {
            $this->min = $x;
            $this->stack[] = $x;

            return;
        }

        if ($x < $this->min) {
            $this->stack[] = 2 * $x - $this->min;
            $this->min = $x;

            return;
        }

        $this->stack[] = $x;
    }

    /**
     * @return NULL
     */
    function pop() {
        $val = end($this->stack);
        unset($this->stack[key($this->stack)]);

        if ($val < $this->min) {
            $this->min = 2 * $this->min - $val;
        }
    }

    /**
     * @return Integer
     */
    function top() {
        $top = end($this->stack);

        if ($top < $this->min) {
            return $this->min;
        }

        return $top;
    }

    /**
     * @return Integer
     */
    function getMin() {
        return $this->min;
    }
}
```
