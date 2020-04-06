# Binary search tree

```js
class Node{
    constructor(data) {
        this.right = null;
        this.left = null;
        this.data = data;
    }
}

class Bst {
    constructor() {
        this.root = null
    }

    /**
     * 1. create a new method called insert which accepts the data as its first argument.
     * 2. declare and initialize the new variable with that data.
     * 3. if the root is empty then set root property to a new node and return it.
     * 4. Declare a new variable called current and initialize with root property.
     * 5. while the current variable is true
     *     - if the data we passed is equal to current.data then return (no duplicates allowed).
     *     - if data is less than current.data and nothing in left it means we need to set current.left to a new node and break the while loop
     *     - if there is left node then update the current variable to current.left.
     *     - if data is greater than current.data and nothing in right it means we need to set current.right to a new node and break the while loop
     *     - if there is right node then update the current variable to current.right.
     *
     * @param  mixed data
     *
     * @return void
     */
    insert(data) {
        var node = new Node(data);

        if (! this.root) {
            this.root = node;

            return this;
        }

        let current = this.root;
        while (current) {
            // duplicates check
            if (data === current.data) {
                return;
            }

            // left node insertion
            if (data < current.data) {
                if (!current.left ) {
                    current.left = node;

                    break;
                }

                current = current.left
            }

            //right node insertion
            if (data > current.data) {
                if (!current.right){
                    current.right = node;

                    break;
                }

                current = current.right
            }
        }
    }

    /**
     * 1. Declare a new method called find which accepts data as its first argument.
     * 2. if the root is empty then return null.
     * 3. declare a new variable and initialize with this.root property.
     * 4. while current is property is true.
     *     - if data is equal to the current. data then return that data.
     *     - if there are current.right and data is greater than current.data then update the current variable with current.right.
     *     - if there are current.left and data is less than current.data then update the current variable with current.left.
     *
     * @param  mixed data
     *
     * @return boolean|mixed
     */
    find(data) {
        if (!this.root) return null;

        let current = this.root;
        while (current) {
            if (data == current.data) return current.data;

            if (current.right && data > current.data) {
                current = current.right
            } else {
                current = current.left
            }
        }

        return false
    }

    /**
     * Check if the data is presen in binary search tree.
     *
     * @param  mixed data
     *
     * @return boolean
     */
    contains(data) {
        const found = this.find(data)

        if (found) {
            return true;
        }

        return false;
    }

    /**
     * 1. Create a new method called bfs.
     * 2. Declare three variables and initialize with a root node, an array with the node, empty array.
     * 3. While the queue is not empty.
     *     - update the node variable with the node from the queue.
     *     - if node.left property is true then push node.left to the queue.
     *     - if node.right property is true then push node.right to the queue.
     *     - push the data to the finalData array.
     * 4. return finalData
     *
     * @return array
     */
    bfs() {
        let node = this.root;
        const queue = [node];
        const finalData = [];

        while(queue.length){
            node = queue.shift();

            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);

            finalData.push(node.data);
        }

        return finalData;
    }
}
```
