# API Reference

[official documentation](https://firebase.google.com/docs/reference/js/firestore_)

## `getFirestore()`

Returns the existing `Firestore` instance that is associated with the provided `FirebaseApp`. If no instance exists, initializes a new instance with default settings.

Signature:

```javascript
export declare function getFirestore(app?: FirebaseApp): Firestore:
```

## `doc(firestore, path, pathSegments)`

Gets a `DocumentReference` instance that refers to the document at the specified absolute path.

Signature:

```typescript
export declare function 
    doc(firestore: Firestore, path: string, ...pathSegments: string[]):
    DocumentReference<DocumentData>;
```

- `firestore`: a reference to the root Firestore instance
- `path`: a slash-separated path to a document
- `pathSegments`: Additional path segments that will be applied relative to the first argument

## `getDoc()`

Reads the document referred to by this `DocumentReference`

Signature:

```javascript
export declare function getDoc<T>(reference: DocumentReference<T>): Promise<DocumentSnapshot<T>>;
```

## `setDoc()`

Writes to the document referred to by this `DocumentReference`. If the document does not yet exists, it will be created.

Signature:

```jsx
export declare function
    setDoc<T>(reference: DocumentReference<T>, data: WithFieldValue<T>):
    Promise<void>;
```

## `exists()`

Returns true if this `DocumentSnapshot` contains any data.
