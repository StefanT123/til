# Knight's dialer

Imagine you place a knight chess piece on a phone dial pad. This chess piece moves in an uppercase “L” shape: two steps horizontally followed by one vertically, or one step horizontally then two vertically.

Suppose you dial keys on the keypad using only hops a knight can make. Every time the knight lands on a key, we dial that key and make another hop. The starting position counts as being dialed.

How many distinct numbers can you dial in N hops from a particular starting position?

```php
class KnightDialer {
    protected $cache = [];

    /*
    Solution using recursive approach
    with memoization.
     */
    public function recursive($position, $hops) {
        if (isset($this->cache[$position][$hops])) {
            return $this->cache[$position][$hops];
        }

        if ($hops === 0) {
            return 1;
        }

        $numOfHops = 0;
        $neighbours = $this->neighbours($position);
        $neighboursLen = count($neighbours);

        for ($i = 0; $i <$neighboursLen; $i++) {
            $numOfHops += $this->recursive($neighbours[$i], $hops - 1);
        }

        $this->cache[$position][$hops] = $numOfHops;

        return $numOfHops;
    }

    /*
    Solution using iterative approach
    with Dynamic Programming.

    This solution is slightly better
    because it uses constant memory.
     */
    public function iterative($position, $hops) {
        $neighbourCase = array_fill(0, 10, 1);
        $numOfHops = 1;

        while ($numOfHops <= $hops) {
            $currentCase = array_fill(0, 10, 0);
            $numOfHops++;

            for ($i = 0; $i < 10; $i++) {
                foreach ($this->neighbours($i) as $neighbour) {
                    $currentCase[$i] += $neighbourCase[$neighbour];
                }
            }

            $neighbourCase = $currentCase;
        }

        return $currentCase[$position];
    }

    protected function neighbours($position) {
        $list = [
            0 => [6, 4],
            1 => [6, 8],
            2 => [9, 7],
            3 => [8, 4],
            4 => [3, 9, 0],
            5 => [],
            6 => [1, 7, 0],
            7 => [2, 6],
            8 => [3, 1],
            9 => [2, 4],
        ];

        return $list[$position];
    }
}


echo (new KnightDialer)->recursive(6, 4);
echo (new KnightDialer)->iterative(6, 4);
```
