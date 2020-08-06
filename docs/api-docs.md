---
title: API Documentation
---

## @simplewebauthn/browser

### `startAttestation`

#### Signature

```ts
startAttestation(creationOptionsJSON): Promise<AttestationCredentialJSON>
```

#### Arguments

- `creationOptionsJSON`: The return value from [`generateAttestationOptions`](#generateattestationoptions)

#### Returns

- `AttestationCredentialJSON` **object**
  - `id` **string**
  - `rawId` **string**
  - `response` **object**
    - `attestationObject` **string**
    - `clientDataJSON`: **string**
  - `type` **"public-key"**

#### Notes

The return value is the exact response from the authenticator with a few `Buffer`'s encoded to base64url. It should be passed straight into [`verifyAttestationResponse`](#verifyattestationresponse) as `options.credential`.

### `startAssertion`

#### Signature

```ts
startAssertion(requestOptionsJSON): Promise<AssertionCredentialJSON>
```

#### Arguments

- `requestOptionsJSON`: The return value from [`generateAssertionOptions()`](#)

#### Returns

- `AssertionCredentialJSON` **object**
  - `id` **string**
  - `rawId` **string**
  - `response` **object**
    - `authenticatorData` **string**
    - `clientDataJSON` **string**
    - `signature` **string**
  - `type` **"public-key"**

#### Notes

The return value is the exact response from the authenticator with a few `Buffer`'s encoded to base64url. It should be passed straight into [`verifyAssertionResponse`](#verifyassertionresponse) as `options.credential`.

### `supportsWebauthn`

#### Signature

```ts
supportsWebauthn(): boolean
```

#### Arguments

- N/A

#### Returns

- `boolean`

#### Notes

A helper method to check for the browser's ability to make WebAuthn API calls. `startAttestation()` and `startAssertion()` both call this method internally. In some scenarios, though, it may be more desirable to hide UI when the page loads and a call to `supportsWebauthn()` returns false:

```html
<script>
  const elemBegin = document.getElementById('btnBegin');
  const elemSuccess = document.getElementById('success');
  const elemError = document.getElementById('error');

  const { startAttestation, supportsWebauthn } = SimpleWebAuthnBrowser;

  if (!supportsWebauthn()) {
    elemBegin.style.display = 'none';
    elemError.innerText = 'It seems this browser does not support WebAuthn...';
  }

  // ...snip...
</script>
```

## Server
