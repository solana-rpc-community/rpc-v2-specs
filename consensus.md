# Consensus domain specifications

## V1 RPC calls
- [getslot](https://docs.solana.com/api/http#getslot)
- [getBlockHeight](https://docs.solana.com/api/http#getblockheight)
- [getblocktime](https://docs.solana.com/api/http#getblocktime)
- [getfirstavailableblock](https://docs.solana.com/api/http#getfirstavailableblock)
- [minimumledgerslot](https://docs.solana.com/api/http#minimumledgerslot) can be merged with getfirstavailableblock
- [getlatestblockhash](https://docs.solana.com/api/http#getlatestblockhash)
- [isblockhashvalid](https://docs.solana.com/api/http#isblockhashvalid)
- [getblockcommitment](https://docs.solana.com/api/http#getblockcommitment) only for the last 150 blocks.
- [getepochinfo](https://docs.solana.com/api/http#getepochinfo)
- [getleaderschedule](https://docs.solana.com/api/http#getleaderschedule)
- [getSlotLeader](https://docs.solana.com/api/http#getslotleader)
- [getSlotLeaders](https://docs.solana.com/api/http#getslotleaders)
- [getvoteaccounts](https://docs.solana.com/api/http#getvoteaccounts)
- [getrecentperformancesamples](https://docs.solana.com/api/http#getrecentperformancesamples)
- [getsignaturesforaddress](https://docs.solana.com/api/http#getsignaturesforaddress) at process commitment.
- [getsignaturestatuses](https://docs.solana.com/api/http#getsignaturestatuses) at process commitment
- [getrecentprioritizationfees](https://docs.solana.com/api/http#getrecentprioritizationfees)
- [getBlockCommitment](https://docs.solana.com/api/http#getblockcommitment) at process commitment.
- [getFirstAvailableBlock](https://docs.solana.com/api/http#getfirstavailableblock)
- [getIdentity](https://docs.solana.com/api/http#getidentity)
- [getMaxRetransmitSlot](https://docs.solana.com/api/http#getmaxretransmitslot)
- [getRecentPrioritizationFees](https://docs.solana.com/api/http#getrecentprioritizationfees)

## V1 Subscriptions
 - [slotSubscribe](https://docs.solana.com/api/websocket#slotsubscribe)
 - [blockSubscribe](https://docs.solana.com/api/websocket#blocksubscribe)
 - [transactionSubscribe](https://github.com/solana-foundation/solana-improvement-documents/pull/69)
 - [logsSubscribe](https://docs.solana.com/api/websocket#logssubscribe)
 - [signatureSubscribe](https://docs.solana.com/api/websocket#signaturesubscribe)
 - [slotsUpdatesSubscribe](https://docs.solana.com/api/websocket#slotsupdatessubscribe)
 - [voteSubscribe](https://docs.solana.com/api/websocket#votesubscribe)

## V2 RPC calls
- [getslot](https://docs.solana.com/api/http#getslot)
- [getepochinfo](https://docs.solana.com/api/http#getepochinfo)
- [getleaderschedule](https://docs.solana.com/api/http#getleaderschedule)
- [getlatestblockhash](https://docs.solana.com/api/http#getlatestblockhash)
- [getBlockHeight](https://docs.solana.com/api/http#getblockheight)
- [getvoteaccounts](https://docs.solana.com/api/http#getvoteaccounts)
- [getsignaturesforaddress](https://docs.solana.com/api/http#getsignaturesforaddress) at process commitment.
- [getsignaturestatuses](https://docs.solana.com/api/http#getsignaturestatuses) at process commitment
- getTransactionsByAddress at process commitment

## V2 Subscriptions
 - [slotSubscribe](https://docs.solana.com/api/websocket#slotsubscribe)
 - [blockSubscribe](https://docs.solana.com/api/websocket#blocksubscribe)
 - [transactionSubscribe](https://github.com/solana-foundation/solana-improvement-documents/pull/69)

## Entities
 - Leader Schedule: Vec<String, Vec<usize>>> : List of slot number per node Id.

## Data source
 - Geyser plugin: Stake account, Vote account, Slot, FullBLock.

