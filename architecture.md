# Architecture

 This page present the way the RPC components can be organized. 

This architecture suppose that RPC call have to works as the V1.

## Key points

Each domain are connected with the others using messages. It allow less dependency and a more flexible set up.

The Router route the client incoming request to the right domains backend

The View format the domains backend answer to the format asked by the clients.

Each domain implements its own access point using the protocol that is the most appropriate (Json, Grpc, GraphQL, ...).

An example of client request routine is presented for the account domain. This is the same for the other domains.

## Diagram

```mermaid
flowchart TD
    subgraph History Domain
        History("History Domain

        at confirm/finalized
            getBlock()
            getTransaction()
            ...
        ")
    end

    subgraph Send Tx Domain
        SendTx("SendTx Domain

              send_transaction()
              ...
        ")
    end

    subgraph Account Domain
        Account("SendTx Domain

            getAccountInfo()
            getProgramAccounts()
              ...
        ")
        AccountSubscription("Subscription
            programSubscribe
        ")
    end

    subgraph Validator Host
        Validator["Solana Validator
            Validator process
            + GRPC Geyser"]
    end

    subgraph Consensus    
        Consensus("RPC calls:
            getVoteAccounts()
            getLeaderSchedule()
            getSlot()
            ...
        ")
        ConsensusSubscription("Subscriptions:
            slotSubscribe
            blockSubscribe
            ...
              ")
    end
    subgraph Cluster Domain
        Cluster("Cluster Sub Domain
            
           getClusterNodes()")
    end
    
    subgraph Router
        AccessRouter("Get client request
           route to the domain 
        ")

        AccesView("Format answer
            return to the client
        ")
    end

    subgraph Client
        RPCClient("Client
            Send a request/subscription
        ")
    end

    Validator-- "geyser Block/Slot" -->Consensus
    Validator-- "geyser Account" -->Account
    Validator-- "Cluster info" -->Cluster
    Account-- "Stake/Vote Account" -->Consensus
    Consensus-- "Block Info/Slot/Leader Schedule" -->SendTx
    Consensus-- "confirmed Tx" -->SendTx
    Cluster-- "Cluster info" -->SendTx
    Consensus-- "Full Block/Slot/Epoch" -->History

    AccessRouter-- "forward request" --> Account
    Account-- "get answer" --> AccesView

    Client<-- "get answer" --> AccessRouter
 
    classDef consensus fill:#1168bd,stroke:#0b4884,color:#ffffff
    classDef history fill:#666,stroke:#0b4884,color:#ffffff
    classDef sendtx fill:#08427b,stroke:#052e56,color:#ffffff
    classDef redgray fill:#62524F, color:#fff
    classDef greengray fill:#4F625B, color:#fff

    class SendTx sendtx
    class History redgray
    class Consensus consensus
    class Cluster greengray
```