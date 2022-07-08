# Understand Cloud Firestore

[API reference](https://firebase.google.com/docs/reference/js/firestore_)
[official documentation](https://firebase.google.com/docs/firestore/data-model)

## References

Every document in Cloud Firestore is uniquely identified by its location within the database.
You can create reference whether or no data exists there.

```javascript
import {doc} from 'firebase/firestore';

const alovelaceDocumentRef = doc(db, 'users', 'alovelace');
```

reference to collections

```javascript
import {collection} from 'firebase/firestore';

const usersCollectionRef = collection(db, 'users');
```

you can also create references by specifying the path to a document or collection as string

```javascript
import {doc} from 'firebase/firestore';

const alovelaceDocumentRef = doc(db, 'users/alovelace');
```

## Add and manage data

ways to write data

- Set the data of a document within a collection, explicitly specifying a document identifier
- Add a new document to a collection. In this case, Firestore automatically generates the document identifier
- create empty document with an automatically generated identifier, and assign data to it later.

### Set a document `set()`

To **create** or **overwrite** a single document, use the `set()` method:
If the document does not exist, it will be created.
If the document exists, its contents will be overwritten with the newly provided data.

```javascript
import {doc, setDoc} from 'firebase/firestore';

// Add a new document in collection "cities"
await setDoc(doc(db, 'cities', 'LA'),{
    name: 'Los Angeles',
    state: 'CA',
    country: 'USA'
});
```

You can specify that data should be merged into the existing document is you do not want to overwrite.

```javascript
import {doc, setDoc} from 'firebase/firestore';

const cityRef = doc(db, 'cities', 'BJ');
setDoc(cityRef, {capital: true}, {merge: true});
```
