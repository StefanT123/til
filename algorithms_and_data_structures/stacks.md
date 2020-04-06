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

Linked list
```js
class Node {
  constructor(next, value) {
    this.next = next
    this.value = value
  }
}

class Stack {
  constructor() {
    this.stack = null
  }

  push(element) {
    let head = this.stack
    let newNode = new Node(null, element)

    if (!head) {
      this.stack = newNode
    } else {
      newNode.next = head
      this.stack = newNode
    }
  }

  pop() {
    let head = this.stack

    if (!head) return 'Stack is empty!'

    this.stack = head.next
    return head.value
  }

  peek() {
    if(!this.stack) return 'Stack is empty!'
    return this.stack.value
  }
}
```
