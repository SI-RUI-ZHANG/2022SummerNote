# API Reference

[official documentation](https://firebase.google.com/docs/reference/js/auth)

## `getAuth()`

Signature:

Returns the Auth instance associated with the provided `FirebaseApp`. If no exists, initializes an Auth instance with platform=specific default dependencies.

Signature:

```jsx
export declare function getAuth(app?: FirebaseApp): Auth;
```

## `GoogleAuthProvider` class

Provider for generating an `OAuthCredential`

```jsx
export declare class GoogleAuthProvider extends BaseOAuthProvider
```

## `signInWithPopup()`

Authenticates a Firebase client using a popup-based OAuth authenticating flow.

If succeeds, returns the signed in user along with the provider's credential. If sign in was unsuccessful, returns an error object containing additional information about the error.

Signature:

```jsx
export declare function
    signInWithPopup(auth: Auth, provider: AuthProvider, resolver?: PopupRedirectResolver)
    : Promise<UserCredential>;
```

Returns: `Promise<UserCredential>`

## `signInWithREdirect()`

Authenticates a Firebase client using a full-page redirect flow

To handle the results and errors for this operation, refer to `getRedirectResult()`

Signature:

```jsx
export declare function
    signInWithRedirect(auth: Auth, provider: AuthProvider, resolver?: PopupRedirectResolver)
    : Promise<never>
```

## `getRedirectResult()`

Returns a `UserCredential` from the redirect-based sign-in flow.

If sign-in succeeded, returns the signed in user. If sign-in was unsuccessful, fails with an error. If no redirect operation was called, returns a `UserCredential` with a null `user`

Signature:

```jsx
export declare function getRedirectResult(auth: Auth, resolver?: PopupRedirectResolver)
    : Promise<UserCredential | null>;
```
