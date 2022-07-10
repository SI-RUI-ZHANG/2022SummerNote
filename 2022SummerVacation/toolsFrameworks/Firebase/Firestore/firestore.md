# firestore

[official documentation](https://firebase.google.com/docs/firestore)

 <img src='../images/9d1e65405e94bbf6b19d3f1fefb031c57fb2526bf4f8ec929a14d4715dbb8945.png' style="width: 40%; display: block; margin: auto">

Fires store use NoSQL data model, you store data in documents that contain fields mapping to value. Those documents are stored in collections, which are containers for your documents that you can use to organize your data and build queries.

## Getting Started

[official documentation](https://firebase.google.com/docs/firestore/quickstart)

### set up development environment

```bash
npm install firebase
```

```javascript
import {initializeApp} from 'firebase/app';
import {getFirestore} from 'firebase/firestore';
```

### Initialize Cloud Firestore

```javascript
import { initializeApp } from "firebase/app";
import { getFirestore } from "firebase/firestore";

// TODO: Replace the following with your app's Firebase project configuration
// See: https://firebase.google.com/docs/web/learn-more#config-object
const firebaseConfig = {
    // ...
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);


// Initialize Cloud Firestore and get a reference to the service
const db = getFirestore(app);
```

### Add data

Cloud Firestore creates collections and documents implicitly the first time you add data to the document. You do not need to explicitly create collections or documents

create a new collection and document using the following example code

```javascript
import {collection, addDoc} from 'firebase/firestore';

try {
    const docRef = await addDoc(collection(db, 'users'), {
        first: 'Ada',
        last: 'Lovelace',
        born: 1895
    });
    console.log("Document written with ID: ", docRef.id);
} catch (e) {
    console.error('Error adding document: ', e);
}
```

Add another document to the `users` collection.
**NOTICE**: this document includes key-value pair (middle name) that does not appear in the first document. Documents in a collection can contain different sets of information

```javascript
// Add a second document with a generated ID.
import {collection, addDoc} from 'firebase/firestore';

try {
    const docRef = await addDoc(collection(db, 'users'), {
        first: 'Alan',
        middle: 'Mathison',
        last: 'Turing',
        born: 1912
    })
    console.log("Document written with ID: ", docRef.id);
} catch (e) {
    console.error('Error adding document: ', e);
}
```

### Read data

```javascript
import {collection, getDocs} from 'firebase/firestore';

const querySnapshot = await getDocs(collection(db, 'users'));
querySnapshot.forEach(doc) => {
    console.log(`${doc.id} => ${doc.data()}`);
}
```
