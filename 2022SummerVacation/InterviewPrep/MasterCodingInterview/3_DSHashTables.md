# Hash Tables

_key-value_ pairs

| operation | time complexity |
| --------- | --------------- |
| insert    | $O(1)$          |
| lookup    | $O(1)$          |
| delete    | $O(1)$          |
| search    | $O(1)$          |

```javascript
let user = {
    age: 54,
    name: 'Kylie',
    magic: true,
    scream() {
        console.log('ahhhhhhh!');
    }
}
```

ES6 `map` allows us to use any type of data as keys, whereas object only allow using strings

```javascript
const a = new Map()
const b = new Sets()
// Sets() only stores keys
```

## Implement A Hash Table

```javascript
class MyHashTable {
    constructor(size) {
        this.data = new Array(size);
    }

    _hash(key) {
        // underscore for private property
        let hash = 0;
        for (let i = 0; i < key.length; i++) {
            hash = (hash + key.charCodeAt(i) * i) % this.data.length;
        }
        return hash;
    }

    set(key, value) {
        let address = this._hash(key);
        if (!this.data[address]) {
            this.data[address] = [];
        }
        this.data[address].push([key, value]);
    }

    get(key) {
        let address = this._hash(key);
        const currentBucket = this.data[address];
        if (currentBucket) {
            for (let bucketKey in currentBucket) {
                if (currentBucket[bucketKey][0] === key) {
                    return currentBucket[bucketKey][0];
                }
            }
        }
        return undefined;
    }

    keys() {
        const keysArray = [];
        for (let i = 0; i < this.data.length; i++) {
            if (this.data[i]) {
                keysArray.push(this.data[i][0][0]);
            }
        }
        return keysArray;
    }
}
```

## Exercise: First Recurring Character

```javascript
function firstRecurring(array) {
    let set = new Set();
    for (let element of array) {
        if (set.has(element)) {
            return element;
        }
        set.add(element);
    }
    return undefined
}
```
