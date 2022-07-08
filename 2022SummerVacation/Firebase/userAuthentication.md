# use authentication (google)

[official documentation](https://firebase.google.com/docs/auth/web/google-signin)

## 1. create instance of the Google provider object

```javascript
import {GoogleAuthProvider} from "firebase/auth";

const provider = new GoogleAuthProvider();
```

## 2. prompt users to sign in

to sign in with a pop-up window, call `signInWithPopup`:

```javascript
import {getAuth, signInWithPopup, GoogleAuthProvider} from 'firebase/auth';

const auth = getAuth();
signInWithPopup(auth, provider)
    .then((result) => {
        // Get Google Access Token, you can use it to access the Google API
        const credential = GoogleAuthProvider.credentialFromResult(result);
        const {accessToken} = credential;
        // The signed-in user info.
        const {user} = result;
    }).catch((error) => {
        // Handle Errors here.
        const errorCode = error.code;
        const errorMessage = error.message;
        // The email of the user's account used
        const {email} = error.customData;
        // the AuthCredential type that was used
        const credential = GoogleAuthProvider.credentialFromError(error);
        // ...
    })
```

to sign in by redirecting to the sign-in page, call `signInWithRedirect`

```javascript
import {getAuth, signInWithRedirect} from 'firebase/auth';

const auth = getAuth();
signInWithRedirect(auth, provider);
```

then, you can retrieve the Google provider's OAuth token by calling `getRedirectResult` when your page loads:

```javascript
import {getAuth, getRedirectResult, GoogleAuthProvider} from 'firebase/auth';

const auth = getAuth();
getRedirectResult(auth)
    .then((result) => {
        // get Google access token
        const credential = GoogleAuthProvider.credentialFromResult(result);
        const {accessToken} = credential;

        // The signed-in user info
        const {user} = result
    }).catch((error) => {
        // Handle Error here.
        const errorCode = error.code;
        const errorMessage = error.message;
        // the email fo hte user's account used
        const {email} = error.customData;
        // The AuthCredential type that was used
        const credential = GoogleAuthProvider.credentialFromError(error);
    })
```
