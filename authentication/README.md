FairX DID Authentication Specification
=================
9th July 2022

# Table of Contents
- [FairX DID Authentication Specification](#fairx-did-authentication-specification)
- [Table of Contents](#table-of-contents)
- [Overview <a name="fairx-did-authentication-overview"></a>](#overview-)
- [Protocol](#protocol)
  - [Initial DID Presentation](#initial-did-presentation)
- [References <a name="fairx-did-authentication-references"></a>](#references-)

FairX is an experimental suite of open source services that run alongside [TBD's Self-Sovereign SDK and Services](https://github.com/TBD54566975). 

FairX Decentralized Identifiers is a distributed identifier (DID) designed to provide a way for FairX Protocol Compliant Nodes to identify and verify participants on its network, as well as provide an identity framework for the FairX Protocol "sessions". The role of a FairX DID is to provide a service that supports authentication, personal information verification, the ability to identify FairX Protocol WASM packages and verify their authenticity.  DIDs and the TBD infrastructure provide the backbone for the FairX Protocol.  

The FairX DID Authentication Specification conforms to the requirements specified in the DID Core Specification [**[1]**](https://www.w3.org/TR/did-core/), currently published by the W3C Credentials Community Group. For more information about DIDs and DID method specifications, please see the DID Primer [**[2]**](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/blob/master/topics-and-advance-readings/did-primer.md).  Specifically, the FairX Protocol relies on the [**[3]**](https://www.w3.org/TR/did-core/#verification-methods) Verification Methods, [**[4]**](https://www.w3.org/TR/did-core/#verification-relationships) Verification Relationships, and [**[5]**](https://www.w3.org/TR/did-core/#services) Services sub-sections of the DID Core Specification.


# Overview <a name="fairx-did-authentication-overview"></a>

The FairX Protocol requires authentication whenever there is node-to-node communication.  The protocol relies on the W3C's [Verification Methods](https://www.w3.org/TR/did-core/#verification-methods) and [Verification Relationships](https://www.w3.org/TR/did-core/#verification-relationships) embedded in a DID Document after resolution in order to express the cryptographic material and methods required to authenticate the DID Subject as specified by their DID.

Once authenticated to a [**[6]**](https://github.com/fairxio/protocol/tree/main/glossary.md#fairx-protocol-glossary-fairx-domain) FairX Domain, a node can use the JWT token returned to interact further with the [**[7]**](https://github.com/fairxio/protocol/tree/main/glossary.md#fairx-protocol-glossary-fairx-node) FairX Node which is registered for that FairX Domain.

# Protocol

![FairX Protocol - Authentication](https://github.com/fairxio/protocol/raw/main/authentication/fairx-protocol-authentication.png "FairX Protocol - Authentication")

## Initial DID Presentation

The DID Subject must first present its DID to the FairX Node authentication service.  This is done according to the [FairX Protocol Open API Authentication Specification]()'s `/auth` endpoint.

The [DID Subject](https://www.w3.org/TR/did-core/#dfn-did-subjects)'s DID Document **must** include the following properties, according to the [DID Core Specification](https://www.w3.org/TR/did-core/):

- A `verificationMethod` property with at least 1 [verification method](https://www.w3.org/TR/did-core/#dfn-verification-method) defined for use in authentication
- A specific [Verification Relationship](https://www.w3.org/TR/did-core/#dfn-verification-relationship) that expresses the relationship between a DID Subject and a Verification Method

# References <a name="fairx-did-authentication-references"></a>

----------

**[1]** https://www.w3.org/TR/did-core/

**[2]** https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/blob/master/topics-and-advance-readings/did-primer.md

**[3]** https://www.w3.org/TR/did-core/#verification-methods

**[4]** https://www.w3.org/TR/did-core/#verification-relationships

**[5]** https://www.w3.org/TR/did-core/#services

**[6]** https://github.com/fairxio/protocol/tree/main/glossary.md#fairx-protocol-glossary-fairx-domain

**[7]** https://datatracker.ietf.org/doc/html/rfc7515