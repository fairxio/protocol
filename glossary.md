# FairX Protocol Glossary

FairX is an experimental suite of open source services that run alongside [TBD's Self-Sovereign SDK and Services](https://github.com/TBD54566975). 

FairX Decentralized Identifiers is a distributed identifier (DID) designed to provide a way for FairX Protocol Compliant Nodes to identify and verify participants on its network, as well as provide an 
identity framework for the FairX Protocol "sessions". The role of a FairX DID is to provide a service that supports authentication, personal information verification, the ability to identify FairX Protocol
WASM packages and verify their authenticity.  DIDs and the TBD infrastructure provide the backbone for the FairX Protocol.  

The FairX Protocol Glossary is a central location to understand terms users in the various FairX Protocol and Sub-Protocol specifications.  All other specifications should link back to this Glossary to help the reader navigate the terminology.

# Table of Contents
- [FairX Protocol Glossary](#fairx-protocol-glossary)
- [Table of Contents](#table-of-contents)
- [Concepts <a name="fairx-protocol-glossary-concepts"></a>](#concepts-)
  - [FairX Domain <a name="fairx-protocol-glossary-fairx-domain"></a>](#fairx-domain-)
  - [FairX Node <a name="fairx-protocol-glossary-fairx-node"></a>](#fairx-node-)

# Concepts <a name="fairx-protocol-glossary-concepts"></a>

## FairX Domain <a name="fairx-protocol-glossary-fairx-domain"></a>

A FairX Domain is a common name service configuration (such as [DNS](https://datatracker.ietf.org/doc/html/rfc1034) (default), but could be [ENS](https://eips.ethereum.org/EIPS/eip-137) or similar).

## FairX Node <a name="fairx-protocol-glossary-fairx-node"></a>

A FairX Node is an electronic service which responds to messages sent to it, or retrieved from it, according to the W3C's [Decentralized Web Node Specification](https://identity.foundation/decentralized-web-node/spec/), alongside with FairX's extensions by way of its [FairX Decentralized Web Node Messages](https://github.com/fairxio/protocol/tree/main/did/messages).