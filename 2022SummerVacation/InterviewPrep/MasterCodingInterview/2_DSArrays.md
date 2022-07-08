# Data Structures

## Arrays

| operation | time complexity |
| --------- | --------------- |
| lookup    | $O(1)$          |
| push      | $O(1)$          |
| insert    | $O(n)$          |
| delete    | $O(n)$          |

```javascript
const strings = ['a', 'b', 'c', 'd']

// push
// (append)
strings.push('e')

// pop
// remove the last element
strings.pop()

// unshift
// insert at the beginning
strings.unshift('x')

console.log(strings)
```

### Implementing An Array

```javascript
class MyArray {
    constructor() {
        this.length = 0;
        this.data = {};
    }

    get(index) {
        return this.data[index];
    }

    push(item) {
        this.data[this.length] = item;
        this.length++;
        return this.length;
    }

    pop() {
        const lastItem = this.data[this.length - 1];
        delete this.data[this.length - 1];
        return lastItem;
    }

    delete(index) {
        const item = this.data[index];
        this.shiftItems(index);
        return item
    }

    shiftItems(index) {
        for (let i = index; i < this.length - 1; i++) {
            this.data[i] = this.data[i+1];
        }
        delete this.data[this.length-1];
        this.length--;
    }
}

const newArray = new MyArray()
newArray.push('hi')
newArray.push('this')
newArray.push('is')
newArray.push('Sirui')
newArray.push('Zhang')
console.log(newArray.get(0))
// hi
console.log(newArray.pop())
// Zhang
console.log(newArray.delete(1))
// this
```

### Exercise: reverse an array

```javascript
function reverse(str) {
    if (!str || str.length < 2 || typeof str !== 'string'){
        return 'invalid input';
    }

    const backwards = [];
    const totalItems = str.length - 1;
    for (let i = totalItems; i >= 0; i--) {
        backwards.push(str[i]);
    }

    return backwards.join('');
}

function reverse2(str) {
    return str.split('').reverse().join('');
}

const reverse3 = (str) => str.split('').reverse().join('');

const reverse4 = (str) => [...str].reverse().join('');
// use the spread operator
```

### Exercise: Merge Sorted Arrays

```javascript
function mergeSortedArrays(array1, array2) {
    const mergedArray = [];
    let index1 = 0;
    let index2 = 0;
    while (array1[index1] || array2[index2]) {
        if (typeof(array1[index1]) === 'undefined' ||
            array2[index2] < array1[index1]) {
            mergedArray.push(array2[index2++]);
        } else {
            mergedArray.push(array1[index1++]);
        }
    }

    return mergedArray
}
console.log(mergeSortedArrays([1, 29, 30], [10, 50]))
```
