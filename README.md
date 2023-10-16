# Solana RPC v2 Specs
A repository for RPC v2 related specifications & documents. This document is work-in-progress and subject to change.

## Objectives
1. Discuss changes to the standard RPC API. [https://docs.solana.com/api/http#json-rpc-api-reference]
2. Create a reference implementation that will support the standard API using common open-source software tools. The primary objectives are API compatibility and vendor configurability. Performance is a secondary concern for the reference implementation because vendor-specific infrastructure will ultimately determine performance.
3. The reference implementation should provide a base level of service for local testing with modular options to scale up for mainnet.

## Overview
### Intended User
Solana developers building the next great web3 app who want to run their own infrastructure.

### Problem
They need reference RPC software that scales from localhost up to a single-location, single-tenant mainnet service.

### Solution
The default configuration is suitable for a local test RPC service. There is also documentation illustrating a single-location, single-tenant mainnet service along with recommended hardware & configuration. Teams building Commercial or large-scale applications can use the reference implementation as a guide for their work -- some assembly required.

### Value Proposition (how much will this cost?)
A typical mainnet solution will be possible on a single high-spec bare metal server running in a professional data center. Additional servers will be required for scaling up or add-on services like the Metaplex DAS Read API.

## Details
### Model View Controller (MVC)
Built using a common MVC architecture for modular and maintainable code.
- Router -- Receive client request, route the request to the appropriate controller, get formatted response from controller, send it to the client. Written as a stand-alone service so it is not tied to load balancer software (HAproxy, NGINX, etc).
- Controller -- Get the request from the router, send it to backend, get the respsonse from the backend, send the response to the view layer for parsing, get the rendered view, and send the response to router to send back to the client.
- Views -- Parse the backend response based on the client request. For example, jsonParsed TX + parsing from Anchor IDL. Requests for the default format of base64 will bypass the view later for better performance.
- Model -- the backend data servers or validator RPC which will return data in base64 format.

### Subject Domains
Solana RPC can be segmented into several subject domains. Each of the domains can be served from separate backends. The domains are:
- sendTX -- methods related to sending and confirming transactions.
- Accounts -- methods used to query accounts by id, program, owner, etc.
- Consensus -- methods related to validator consensus (leader schedule, stakes, vote accounts, etc.)
- History -- query transactions and blocks back to genesis
- Cluster -- metadata related to cluster performance, health, etc.

## Contributors
- [Ellipsis Labs](https://ellipsislabs.xyz/)
- [Helium](https://www.helium.com/)
- [Helius](https://helius.xyz)
- [Mango Markets](https://mango.markets)
- [Sniper Labs](https://www.sniper.xyz/)
- [Solana Foundation](https://solana.org)
- [Triton One](https://www.triton.one)
