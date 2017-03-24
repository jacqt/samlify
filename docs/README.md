[express-saml2](https://github.com/tngan/express-saml2)
=======
express-saml2 is a high-level API library for Single Sign On with SAML 2.0

This module provides a library for scaling Single Sign On implementation. Developers can easily configure the entities by importing the metadata. 

We provide a simple interface that's highly configurable.


### Installation
To install the stable version

```bash
$ npm install express-saml2
```

or

```bash
$ yarn add express-saml2
```

### Use cases

+ IdP-initiated Single Sign On
+ IdP-initiated Single Log-out
+ SP-initiated Single Sign On
+ SP-initiated Single Log-out (in development)

Simple solution of Identity Provider is provided in this module for test and educational use. Work with other 3rd party Identity Provider is also supported.

### Glimpse of code

!> **API is changed since v2. All file attributes like metadata and keyFile, it's expected to be normalized as string. It allows easy integration with database storage and import from local file system.**

!> **The constructor of entity is also modified to accept a single configuration object instead of putting metadata and advanced configurations in separate arguments.**

```javascript
const saml = require('express-saml2');
// configure a service provider
const sp = saml.ServiceProvider({
  metadata: fs.readFileSync('./metadata_sp.xml')
});
// configure the corresponding identity provider
const idp = saml.IdentityProvider({
  metadata: fs.readFileSync('./metadata_idp.xml')
});
// parse when receive a SAML Response from IdP
router.post('/acs', (req, res) => {
  sp.parseLoginResponse(idp, 'post', req)
  .then(parseResult => {
    // Write your own validation and render function here
  })
  .catch(console.error);
});
	```

Our default validation is to validate signature and the issuer name of Identity Provider. The code base is self explained. More use cases are provided in this documentation to fit in the real world application.

### License

MIT