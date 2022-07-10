# The Node.js Event emitter

`events` module offers the `EventEmitter` class, which we'll use to handle our events.

Initialize:

```javascript
const EventEmitter = require('events');
const eventEmitter = new EventEmitter();
```

The object exposes, among many others, the `on` and `emit` methods

==Example==

```javascript
eventEmitter.on('start', () => {
    console.log('started');
})
```

when we run

```javascript
eventEmitter.emit('start');
```

the event handler function is triggered, and we get the console log.

You can pass arguments to the event handler by passing them as additional arguments to `emit()`

```javascript
eventEmitter.on('start', number => {
    console.log(`started ${number}`);
})

eventEmitter.emit('start', 23);
```

Multiple arguments

```javascript
eventEmitter.on('start', (start, end) => {
    console.log(`started from ${start} to ${end}`);
})

eventEmitter.emit('start', 1, 100);
```
