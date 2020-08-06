---
title: API Documentation
---

## Browser

### `startAttestation`

#### Signature

```ts
startAttestation(creationOptionsJSON): void
```

#### Arguments

- `creationOptionsJSON`: The return value from [@simplewebauthn/server's `generateAttestationOptions()`](packages/server.md#1-generate-attestation-options)

### `startAssertion(requestOptionsJSON)`

Arguments

- `requestOptionsJSON`: The return value from [@simplewebauthn/server's `generateAssertionOptions()`](packages/server.md#1-generate-assertion-options)

### `supportsWebauthn()`

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
