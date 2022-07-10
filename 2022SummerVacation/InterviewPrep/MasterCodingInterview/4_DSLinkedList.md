# Linked Lists

| operation | time complexity |
| --------- | --------------- |
| prepend   | $O(1)$          |
| append    | $O(1)$          |
| lookup    | $O(n)$          |
| insert    | $O(n)$          |
| delete    | $O(n)$          |

## Implement Singly Linked List

```javascript
class LinkedList {
    constructor(value) {
        this.head = new Node(value)
        this.tail = this.head;
        this.length = 1;
    }

    append(value) {
        const newNode = new Node(value);
        this.tail.next = newNode;
        this.tail = newNode;
        this.length++;
        return this.printList();
    }

    prepend(value) {
        const newNode = new Node(value);
        newNode.next = this.head;
        this.head = newNode;
        this.length++;
        return this.printList();
    }

    printList() {
        const array = [];
        let currentNode = this.head;
        while (currentNode !== null) {
            array.push(currentNode.value);
            currentNode = currentNode.next;
        }
        return array
    }

    traverseToIndex(index) {
        // check params

        let counter = 0;
        let currentNode = this.head;
        while (counter !== index) {
            currentNode = currentNode.next;
            counter++;
        }
        return currentNode;
    }

    insert(index, value) {
        // check params
        if (index >= this.length) {
            return this.append(value);
        }

        if (index !== 0) {
            const newNode = new Node(value);
            const leader = this.traverseToIndex(index - 1);
            const holdingPointer = leader.next;
            leader.next = newNode;
            newNode.next = holdingPointer;
            this.length++;
        } else {
            this.prepend(value)
        }
        return this.printList();
    }

    remove(index) {
        // check params

        if (index !== 0) {
            const leader = this.traverseToIndex(index - 1);
            const unwanted = leader.next;
            leader.next = unwanted.next;
        } else {
            this.head = this.head.next;
        }
        this.length--;
        return this.printList();
    }
}

```

## Implement Doubly Linked List

```javascript
...
```

## Exercise `reverse()`

```javascript
// inside LinkedList class

    reverse() {
        if (!this.head.next) {
            return this.printList();
        }
        let first = this.head;
        this.tail = first;
        let second = this.next;
        while (second) {
           const temp = second.next;
           second.next = first;
           first = second;
           second = temp
        }
        this.head.next = null;
        this.head = first;
    }

// inside LinkedList class

```

