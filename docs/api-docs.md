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

The return value is the [exact attestation response from the authenticator](https://w3c.github.io/webauthn/#iface-authenticatorattestationresponse), with its `ArrayBuffer`'s encoded to base64url strings for ease of transportation back to the server as JSON. The entire object should be passed as-is into [`verifyAttestationResponse`](#verifyattestationresponse) as `options.credential`.

### `startAssertion`

#### Signature

```ts
startAssertion(requestOptionsJSON): Promise<AssertionCredentialJSON>
```

#### Arguments

- `requestOptionsJSON`: The return value from [`generateassertionoptions`](#)

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

The return value is the [exact assertion response from the authenticator](https://w3c.github.io/webauthn/#iface-authenticatorassertionresponse), with its `ArrayBuffer`'s encoded to base64url strings for ease of transportation back to the server as JSON. The entire object should be passed as-is into [`verifyAssertionResponse`](#verifyassertionresponse) as `options.credential`.

### `supportsWebauthn`

#### Signature

```ts
supportsWebauthn(): boolean
```

#### Arguments

- N/A

#### Returns

- **boolean**

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

## @simplewebauthn/server

### `generateAttestationOptions`

#### Signature

```ts
```

#### Arguments

#### Returns

#### Notes

### `verifyAttestationResponse`

#### Signature

```ts
```

#### Arguments

#### Returns

#### Notes

### `generateAssertionOptions`

#### Signature

```ts
```

#### Arguments

#### Returns

#### Notes

### `verifyAssertionResponse`

#### Signature

```ts
```

#### Arguments

#### Returns

#### Notes
