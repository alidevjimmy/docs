---
title: JsonRPC API Reference
weight: 3
---

Each node in the Pactus network can
 be configured to use the [JSON-RPC 2.0](https://www.jsonrpc.org/specification) protocol for communication.
Here you can find the list of all JSON-RPC methods and messages.

All the amounts and values in JSON-RPC endpoints are in
NanoPAC units, which are atomic and the smallest unit in the Pactus blockchain.
Each PAC is equivalent to
1,000,000,000 or 10<sup>9</sup> NanoPACs.

<h2>Methods</h2>

<a href="#pactus.transaction.get_transaction">pactus.transaction.get_transaction</a>

<a href="#pactus.transaction.calculate_fee">pactus.transaction.calculate_fee</a>

<a href="#pactus.transaction.broadcast_transaction">pactus.transaction.broadcast_transaction</a>

<a href="#pactus.transaction.get_raw_transfer_transaction">pactus.transaction.get_raw_transfer_transaction</a>

<a href="#pactus.transaction.get_raw_bond_transaction">pactus.transaction.get_raw_bond_transaction</a>

<a href="#pactus.transaction.get_raw_unbond_transaction">pactus.transaction.get_raw_unbond_transaction</a>

<a href="#pactus.transaction.get_raw_withdraw_transaction">pactus.transaction.get_raw_withdraw_transaction</a>

<a href="#pactus.blockchain.get_block">pactus.blockchain.get_block</a>

<a href="#pactus.blockchain.get_block_hash">pactus.blockchain.get_block_hash</a>

<a href="#pactus.blockchain.get_block_height">pactus.blockchain.get_block_height</a>

<a href="#pactus.blockchain.get_blockchain_info">pactus.blockchain.get_blockchain_info</a>

<a href="#pactus.blockchain.get_consensus_info">pactus.blockchain.get_consensus_info</a>

<a href="#pactus.blockchain.get_account">pactus.blockchain.get_account</a>

<a href="#pactus.blockchain.get_validator">pactus.blockchain.get_validator</a>

<a href="#pactus.blockchain.get_validator_by_number">pactus.blockchain.get_validator_by_number</a>

<a href="#pactus.blockchain.get_validator_addresses">pactus.blockchain.get_validator_addresses</a>

<a href="#pactus.blockchain.get_public_key">pactus.blockchain.get_public_key</a>

<a href="#pactus.network.get_network_info">pactus.network.get_network_info</a>

<a href="#pactus.network.get_node_info">pactus.network.get_node_info</a>

<a href="#pactus.wallet.create_wallet">pactus.wallet.create_wallet</a>

<a href="#pactus.wallet.load_wallet">pactus.wallet.load_wallet</a>

<a href="#pactus.wallet.unload_wallet">pactus.wallet.unload_wallet</a>

<a href="#pactus.wallet.lock_wallet">pactus.wallet.lock_wallet</a>

<a href="#pactus.wallet.unlock_wallet">pactus.wallet.unlock_wallet</a>

<a href="#pactus.wallet.get_total_balance">pactus.wallet.get_total_balance</a>

<a href="#pactus.wallet.sign_raw_transaction">pactus.wallet.sign_raw_transaction</a>

<a href="#pactus.wallet.get_validator_address">pactus.wallet.get_validator_address</a>

<a href="#pactus.wallet.get_new_address">pactus.wallet.get_new_address</a>

<a href="#pactus.wallet.get_address_history">pactus.wallet.get_address_history</a>

<hr/>

<p id="pactus.transaction.get_transaction"></p>
<h3>pactus.transaction.get_transaction <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.transaction.get_transaction retrieves transaction details based on the provided request
parameters.

<h3>Parameters</h3>
<pre>
<code>
{
 "id": "str", // (string) Transaction ID.
 "verbosity": "TRANSACTION_DATA or TRANSACTION_INFO" // (string) Verbosity level for transaction details.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "block_height": n, // (numeric) Height of the block containing the transaction.
 "block_time": n, // (numeric) Time of the block containing the transaction.
 "transaction": { // (json object) Information about the transaction.
  "bond": { // (json object) Bond payload.
   "receiver": "str", // (string) Receiver's address.
   "sender": "str", // (string) Sender's address.
   "stake": n // (numeric) Stake amount in NanoPAC.
  },
  "data": "str", // (string) Transaction data.
  "fee": n, // (numeric) Transaction fee in NanoPAC.
  "id": "str", // (string) Transaction ID.
  "lock_time": n, // (numeric) Lock time for the transaction.
  "memo": "str", // (string) Transaction memo.
  "payload_type": "UNKNOWN or TRANSFER_PAYLOAD or BOND_PAYLOAD
  or SORTITION_PAYLOAD or UNBOND_PAYLOAD or WITHDRAW_PAYLOAD", // (string) Type of transaction payload.
  "public_key": "str", // (string) Public key associated with the transaction.
  "signature": "str", // (string) Transaction signature.
  "sortition": { // (json object) Sortition payload.
   "address": "str", // (string) Address associated with the sortition.
   "proof": "str" // (string) Proof for the sortition.
  },
  "transfer": { // (json object) Transfer payload.
   "amount": n, // (numeric) Transaction amount in NanoPAC.
   "receiver": "str", // (string) Receiver's address.
   "sender": "str" // (string) Sender's address.
  },
  "unbond": { // (json object) Unbond payload.
   "validator": "str" // (string) Address of the validator to unbond from.
  },
  "value": n, // (numeric) Transaction value in NanoPAC.
  "version": n, // (numeric) Transaction version.
  "withdraw": { // (json object) Withdraw payload.
   "amount": n, // (numeric) Withdrawal amount in NanoPAC.
   "from": "str", // (string) Address to withdraw from.
   "to": "str" // (string) Address to withdraw to.
  }
 }
}
</pre>
<hr/>

<p id="pactus.transaction.calculate_fee"></p>
<h3>pactus.transaction.calculate_fee <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.transaction.calculate_fee calculates the transaction fee based on the specified amount
and payload type.

<h3>Parameters</h3>
<pre>
<code>
{
 "amount": n, // (numeric) Transaction amount in NanoPAC.
 "fixed_amount": true|false, // (boolean) Indicates
 that amount should be fixed and includes the fee.
 "payload_type": "UNKNOWN or TRANSFER_PAYLOAD or
  BOND_PAYLOAD or SORTITION_PAYLOAD or UNBOND_PAYLOAD or WITHDRAW_PAYLOAD" // (string) Type of transaction payload.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "amount": n, // (numeric) Calculated amount in NanoPAC.
 "fee": n // (numeric) Calculated transaction fee in NanoPAC.
}
</pre>
<hr/>

<p id="pactus.transaction.broadcast_transaction"></p>
<h3>pactus.transaction.broadcast_transaction <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.transaction.broadcast_transaction broadcasts a signed transaction to the network.

<h3>Parameters</h3>
<pre>
<code>
{
 "signed_raw_transaction": "str" // (string) Signed raw transaction data.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "id": "str" // (string) Transaction ID.
}
</pre>
<hr/>

<p id="pactus.transaction.get_raw_transfer_transaction"></p>
<h3>pactus.transaction.get_raw_transfer_transaction <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.transaction.get_raw_transfer_transaction retrieves raw details of a transfer transaction.

<h3>Parameters</h3>
<pre>
<code>
{
 "amount": n, // (numeric) Transfer amount in NanoPAC.\nIt should be greater than 0.
 "fee": n, // (numeric) Transaction fee in NanoPAC.\nIf not explicitly set, it is calculated based on the amount.
 "lock_time": n, // (numeric) Lock time for the transaction.\nIf not explicitly set, it sets to the last block height.
 "memo": "str", // (string) Transaction memo.
 "receiver": "str", // (string) Receiver's account address.
 "sender": "str" // (string) Sender's account address.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "raw_transaction": "str" // (string) Raw transaction data.
}
</pre>
<hr/>

<p id="pactus.transaction.get_raw_bond_transaction"></p>
<h3>pactus.transaction.get_raw_bond_transaction <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.transaction.get_raw_bond_transaction retrieves raw details of a bond transaction.

<h3>Parameters</h3>
<pre>
<code>
{
 "fee": n, // (numeric) Transaction fee in NanoPAC.\nIf not explicitly set, it is calculated based on the stake.
 "lock_time": n, // (numeric) Lock time for the transaction.\nIf not explicitly set, it sets to the last block height.
 "memo": "str", // (string) Transaction memo.
 "public_key": "str", // (string) Public key of the validator.
 "receiver": "str", // (string) Receiver's validator address.
 "sender": "str", // (string) Sender's account address.
 "stake": n // (numeric) Stake amount in NanoPAC.\nIt should be greater than 0.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "raw_transaction": "str" // (string) Raw transaction data.
}
</pre>
<hr/>

<p id="pactus.transaction.get_raw_unbond_transaction"></p>
<h3>pactus.transaction.get_raw_unbond_transaction <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.transaction.get_raw_unbond_transaction retrieves raw details of an unbond transaction.

<h3>Parameters</h3>
<pre>
<code>
{
 "lock_time": n, // (numeric) Lock time for the transaction.\nIf not explicitly set, it sets to the last block height.
 "memo": "str", // (string) Transaction memo.
 "validator_address": "str" // (string) Address of the validator to unbond from.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "raw_transaction": "str" // (string) Raw transaction data.
}
</pre>
<hr/>

<p id="pactus.transaction.get_raw_withdraw_transaction"></p>
<h3>pactus.transaction.get_raw_withdraw_transaction <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.transaction.get_raw_withdraw_transaction retrieves raw details of a withdraw transaction.

<h3>Parameters</h3>
<pre>
<code>
{
 "account_address": "str", // (string) Address of the account to withdraw to.
 "amount": n, // (numeric) Withdrawal amount in NanoPAC.\nIt should be greater than 0.
 "fee": n, // (numeric) Transaction fee in NanoPAC.\nIf not explicitly set, it is calculated based on the amount.
 "lock_time": n, // (numeric) Lock time for the transaction.\nIf not explicitly set, it sets to the last block height.
 "memo": "str", // (string) Transaction memo.
 "validator_address": "str" // (string) Address of the validator to withdraw from.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "raw_transaction": "str" // (string) Raw transaction data.
}
</pre>
<hr/>

<p id="pactus.blockchain.get_block"></p>
<h3>pactus.blockchain.get_block <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.blockchain.get_block retrieves information about a block based on the provided request
parameters.

<h3>Parameters</h3>
<pre>
<code>
{
 "height": n, // (numeric) Height of the block.
 "verbosity": "BLOCK_DATA or BLOCK_INFO or BLOCK_TRANSACTIONS" // (string) Verbosity level for block information.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "block_time": n, // (numeric) Block timestamp.
 "data": "str", // (string) Block data, only available if the verbosity level is set to BLOCK_DATA.
 "hash": "str", // (string) Hash of the block.
 "header": { // (json object) Block header information.
  "prev_block_hash": "str", // (string) Hash of the previous block.
  "proposer_address": "str", // (string) Address of the proposer of the block.
  "sortition_seed": "str", // (string) Sortition seed of the block.
  "state_root": "str", // (string) State root of the block.
  "version": n // (numeric) Block version.
 },
 "height": n, // (numeric) Height of the block.
 "prev_cert": { // (json object) Certificate information of the previous block.
  "absentees": [ // (json array) List of absentees in the certificate.
   n,
   ...
  ],
  "committers": [ // (json array) List of committers in the certificate.
   n,
   ...
  ],
  "hash": "str", // (string) Hash of the certificate.
  "round": n, // (numeric) Round of the certificate.
  "signature": "str" // (string) Certificate signature.
 },
 "txs": [ // (json array) List of transactions
 in the block.\nTransaction information is available when the verbosity level is set to BLOCK_TRANSACTIONS.
  {
   "bond": { // (json object) Bond payload.
    "receiver": "str", // (string) Receiver's address.
    "sender": "str", // (string) Sender's address.
    "stake": n // (numeric) Stake amount in NanoPAC.
   },
   "data": "str", // (string) Transaction data.
   "fee": n, // (numeric) Transaction fee in NanoPAC.
   "id": "str", // (string) Transaction ID.
   "lock_time": n, // (numeric) Lock time for the transaction.
   "memo": "str", // (string) Transaction memo.
   "payload_type": "UNKNOWN or TRANSFER_PAYLOAD
    or BOND_PAYLOAD or SORTITION_PAYLOAD or UNBOND_PAYLOAD or WITHDRAW_PAYLOAD", // (string) Type of transaction payload.
   "public_key": "str", // (string) Public key associated with the transaction.
   "signature": "str", // (string) Transaction signature.
   "sortition": { // (json object) Sortition payload.
    "address": "str", // (string) Address associated with the sortition.
    "proof": "str" // (string) Proof for the sortition.
   },
   "transfer": { // (json object) Transfer payload.
    "amount": n, // (numeric) Transaction amount in NanoPAC.
    "receiver": "str", // (string) Receiver's address.
    "sender": "str" // (string) Sender's address.
   },
   "unbond": { // (json object) Unbond payload.
    "validator": "str" // (string) Address of the validator to unbond from.
   },
   "value": n, // (numeric) Transaction value in NanoPAC.
   "version": n, // (numeric) Transaction version.
   "withdraw": { // (json object) Withdraw payload.
    "amount": n, // (numeric) Withdrawal amount in NanoPAC.
    "from": "str", // (string) Address to withdraw from.
    "to": "str" // (string) Address to withdraw to.
   }
  },
  ...
 ]
}
</pre>
<hr/>

<p id="pactus.blockchain.get_block_hash"></p>
<h3>pactus.blockchain.get_block_hash <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.blockchain.get_block_hash retrieves the hash of a block at the specified height.

<h3>Parameters</h3>
<pre>
<code>
{
 "height": n // (numeric) Height of the block.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "hash": "str" // (string) Hash of the block.
}
</pre>
<hr/>

<p id="pactus.blockchain.get_block_height"></p>
<h3>pactus.blockchain.get_block_height <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.blockchain.get_block_height retrieves the height of a block with the specified hash.

<h3>Parameters</h3>
<pre>
<code>
{
 "hash": "str" // (string) Hash of the block.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "height": n // (numeric) Height of the block.
}
</pre>
<hr/>

<p id="pactus.blockchain.get_blockchain_info"></p>
<h3>pactus.blockchain.get_blockchain_info <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.blockchain.get_blockchain_info retrieves general information about the blockchain.

<h3>Parameters</h3>
<pre>
<code>
{}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "committee_power": n, // (numeric) Power of the committee.
 "committee_validators": [ // (json array) List of committee validators.
  {
   "address": "str", // (string) Address of the validator.
   "availability_score": n, // (numeric) Availability score of the validator.
   "data": "str", // (string) Validator data.
   "hash": "str", // (string) Hash of the validator.
   "last_bonding_height": n, // (numeric) Last bonding height.
   "last_sortition_height": n, // (numeric) Last sortition height.
   "number": n, // (numeric) Validator number.
   "public_key": "str", // (string) Public key of the validator.
   "stake": n, // (numeric) Validator stake in NanoPAC.
   "unbonding_height": n // (numeric) Unbonding height.
  },
  ...
 ],
 "last_block_hash": "str", // (string) Hash of the last block.
 "last_block_height": n, // (numeric) Height of the last block.
 "total_accounts": n, // (numeric) Total number of accounts.
 "total_power": n, // (numeric) Total power in the blockchain.
 "total_validators": n // (numeric) Total number of validators.
}
</pre>
<hr/>

<p id="pactus.blockchain.get_consensus_info"></p>
<h3>pactus.blockchain.get_consensus_info <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.blockchain.get_consensus_info retrieves information about the consensus instances.

<h3>Parameters</h3>
<pre>
<code>
{}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "instances": [ // (json array) List of consensus instances.
  {
   "Active": true|false, // (boolean) Whether the consensus instance is active.
   "address": "str", // (string) Address of the consensus instance.
   "height": n, // (numeric) Height of the consensus instance.
   "round": n, // (numeric) Round of the consensus instance.
   "votes": [ // (json array) List of votes in the consensus instance.
    {
     "block_hash": "str", // (string) Hash of the block being voted on.
     "cp_round": n, // (numeric) Consensus round of the vote.
     "cp_value": n, // (numeric) Consensus value of the vote.
     "round": n, // (numeric) Round of the vote.
     "type": "VOTE_UNKNOWN or VOTE_PREPARE or VOTE_PRECOMMIT or VOTE_CHANGE_PROPOSER", // (string) Type of the vote.
     "voter": "str" // (string) Voter's address.
    },
    ...
   ]
  },
  ...
 ]
}
</pre>
<hr/>

<p id="pactus.blockchain.get_account"></p>
<h3>pactus.blockchain.get_account <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.blockchain.get_account retrieves information about an account based on the provided
address.

<h3>Parameters</h3>
<pre>
<code>
{
 "address": "str" // (string) Address of the account.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "account": { // (json object) Account information.
  "address": "str", // (string) Address of the account.
  "balance": n, // (numeric) Account balance in NanoPAC.
  "data": "str", // (string) Account data.
  "hash": "str", // (string) Hash of the account.
  "number": n // (numeric) Account number.
 }
}
</pre>
<hr/>

<p id="pactus.blockchain.get_validator"></p>
<h3>pactus.blockchain.get_validator <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.blockchain.get_validator retrieves information about a validator based on the provided
address.

<h3>Parameters</h3>
<pre>
<code>
{
 "address": "str" // (string) Address of the validator.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "validator": { // (json object) Validator information.
  "address": "str", // (string) Address of the validator.
  "availability_score": n, // (numeric) Availability score of the validator.
  "data": "str", // (string) Validator data.
  "hash": "str", // (string) Hash of the validator.
  "last_bonding_height": n, // (numeric) Last bonding height.
  "last_sortition_height": n, // (numeric) Last sortition height.
  "number": n, // (numeric) Validator number.
  "public_key": "str", // (string) Public key of the validator.
  "stake": n, // (numeric) Validator stake in NanoPAC.
  "unbonding_height": n // (numeric) Unbonding height.
 }
}
</pre>
<hr/>

<p id="pactus.blockchain.get_validator_by_number"></p>
<h3>pactus.blockchain.get_validator_by_number <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.blockchain.get_validator_by_number retrieves information about a validator based on the
provided number.

<h3>Parameters</h3>
<pre>
<code>
{
 "number": n // (numeric) Validator number.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "validator": { // (json object) Validator information.
  "address": "str", // (string) Address of the validator.
  "availability_score": n, // (numeric) Availability score of the validator.
  "data": "str", // (string) Validator data.
  "hash": "str", // (string) Hash of the validator.
  "last_bonding_height": n, // (numeric) Last bonding height.
  "last_sortition_height": n, // (numeric) Last sortition height.
  "number": n, // (numeric) Validator number.
  "public_key": "str", // (string) Public key of the validator.
  "stake": n, // (numeric) Validator stake in NanoPAC.
  "unbonding_height": n // (numeric) Unbonding height.
 }
}
</pre>
<hr/>

<p id="pactus.blockchain.get_validator_addresses"></p>
<h3>pactus.blockchain.get_validator_addresses <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.blockchain.get_validator_addresses retrieves a list of all validator addresses.

<h3>Parameters</h3>
<pre>
<code>
{}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "addresses": [ // (json array) List of validator addresses.
  "str",
  ...
 ]
}
</pre>
<hr/>

<p id="pactus.blockchain.get_public_key"></p>
<h3>pactus.blockchain.get_public_key <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.blockchain.get_public_key retrieves the public key of an account based on the provided
address.

<h3>Parameters</h3>
<pre>
<code>
{
 "address": "str" // (string) Address for which public key is requested.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "public_key": "str" // (string) Public key of the account.
}
</pre>
<hr/>

<p id="pactus.network.get_network_info"></p>
<h3>pactus.network.get_network_info <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.network.get_network_info retrieves information about the overall network.

<h3>Parameters</h3>
<pre>
<code>
{}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "connected_peers": [ // (json array) List of connected peers.
  {
   "address": "str", // (string) Network address of the peer.
   "agent": "str", // (string) Agent information of the peer.
   "completed_sessions": n, // (numeric) Completed sessions with the peer.
   "consensus_address": [ // (json array) Consensus address of the peer.
    "str",
    ...
   ],
   "consensus_keys": [ // (json array) Consensus keys used by the peer.
    "str",
    ...
   ],
   "direction": "str", // (string) Direction of connection with the peer.
   "height": n, // (numeric) Height of the peer in the blockchain.
   "invalid_messages": n, // (numeric) Count of invalid messages received.
   "last_block_hash": "str", // (string) Hash of the last block the peer knows.
   "last_received": n, // (numeric) Timestamp of the last received message.
   "last_sent": n, // (numeric) Timestamp of the last sent message.
   "moniker": "str", // (string) Moniker of the peer.
   "peer_id": "str", // (string) Peer ID of the peer.
   "protocols": [ // (json array) List of protocols supported by the peer.
    "str",
    ...
   ],
   "received_bytes": { // (key:value json object) Bytes received per message type.
    ...: ...,
    n: n
   },
   "received_messages": n, // (numeric) Count of received messages.
   "sent_bytes": { // (key:value json object) Bytes sent per message type.
    ...: ...,
    n: n
   },
   "services": n, // (numeric) Services provided by the peer.
   "status": n, // (numeric) Status of the peer.
   "total_sessions": n // (numeric) Total sessions with the peer.
  },
  ...
 ],
 "connected_peers_count": n, // (numeric) Number of connected peers.
 "network_name": "str", // (string) Name of the network.
 "received_bytes": { // (key:value json object) Bytes received per peer ID.
  ...: ...,
  n: n
 },
 "sent_bytes": { // (key:value json object) Bytes sent per peer ID.
  ...: ...,
  n: n
 },
 "total_received_bytes": n, // (numeric) Total bytes received across the network.
 "total_sent_bytes": n // (numeric) Total bytes sent across the network.
}
</pre>
<hr/>

<p id="pactus.network.get_node_info"></p>
<h3>pactus.network.get_node_info <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.network.get_node_info retrieves information about a specific node in the network.

<h3>Parameters</h3>
<pre>
<code>
{}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "addrs": [ // (json array) List of addresses associated with the node.
  "str",
  ...
 ],
 "agent": "str", // (string) Agent information of the node.
 "moniker": "str", // (string) Moniker of the node.
 "peer_id": "str", // (string) Peer ID of the node.
 "protocols": [ // (json array) List of protocols supported by the node.
  "str",
  ...
 ],
 "reachability": "str", // (string) Reachability status of the node.
 "services": [ // (json array) List of services provided by the node.
  n,
  ...
 ],
 "services_names": [ // (json array) Names of services provided by the node.
  "str",
  ...
 ],
 "started_at": n // (numeric) Timestamp when the node started.
}
</pre>
<hr/>

<p id="pactus.wallet.create_wallet"></p>
<h3>pactus.wallet.create_wallet <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.wallet.create_wallet creates a new wallet with the specified parameters.

<h3>Parameters</h3>
<pre>
<code>
{
 "language": "str", // (string) Language for the mnemonic.
 "mnemonic": "str", // (string) Mnemonic for wallet recovery.
 "password": "str", // (string) Password for securing the wallet.
 "wallet_name": "str" // (string) Name of the new wallet.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "wallet_name": "str" // (string) Name of the created wallet.
}
</pre>
<hr/>

<p id="pactus.wallet.load_wallet"></p>
<h3>pactus.wallet.load_wallet <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.wallet.load_wallet loads an existing wallet with the given name.

<h3>Parameters</h3>
<pre>
<code>
{
 "wallet_name": "str" // (string) Name of the wallet to load.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "wallet_name": "str" // (string) Name of the loaded wallet.
}
</pre>
<hr/>

<p id="pactus.wallet.unload_wallet"></p>
<h3>pactus.wallet.unload_wallet <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.wallet.unload_wallet unloads a currently loaded wallet with the specified name.

<h3>Parameters</h3>
<pre>
<code>
{
 "wallet_name": "str" // (string) Name of the wallet to unload.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "wallet_name": "str" // (string) Name of the unloaded wallet.
}
</pre>
<hr/>

<p id="pactus.wallet.lock_wallet"></p>
<h3>pactus.wallet.lock_wallet <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.wallet.lock_wallet locks a currently loaded wallet with the provided password and
timeout.

<h3>Parameters</h3>
<pre>
<code>
{
 "wallet_name": "str" // (string) Name of the wallet to lock.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "wallet_name": "str" // (string) Name of the locked wallet.
}
</pre>
<hr/>

<p id="pactus.wallet.unlock_wallet"></p>
<h3>pactus.wallet.unlock_wallet <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.wallet.unlock_wallet unlocks a locked wallet with the provided password and
timeout.

<h3>Parameters</h3>
<pre>
<code>
{
 "password": "str", // (string) Password for unlocking the wallet.
 "timeout": n, // (numeric) Timeout duration for the unlocked state.
 "wallet_name": "str" // (string) Name of the wallet to unlock.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "wallet_name": "str" // (string) Name of the unlocked wallet.
}
</pre>
<hr/>

<p id="pactus.wallet.get_total_balance"></p>
<h3>pactus.wallet.get_total_balance <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.wallet.get_total_balance returns the total available balance of the wallet.

<h3>Parameters</h3>
<pre>
<code>
{
 "wallet_name": "str" // (string) Name of the wallet.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "total_balance": n, // (numeric) The total balance of the wallet in NanoPAC.
 "wallet_name": "str" // (string) Name of the wallet.
}
</pre>
<hr/>

<p id="pactus.wallet.sign_raw_transaction"></p>
<h3>pactus.wallet.sign_raw_transaction <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.wallet.sign_raw_transaction signs a raw transaction for a specified wallet.

<h3>Parameters</h3>
<pre>
<code>
{
 "password": "str", // (string) Password for unlocking the wallet for signing.
 "raw_transaction": "str", // (string) Raw transaction data to be signed.
 "wallet_name": "str" // (string) Name of the wallet used for signing.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "signed_raw_transaction": "str", // (string) Signed raw transaction data.
 "transaction_id": "str" // (string) ID of the signed transaction.
}
</pre>
<hr/>

<p id="pactus.wallet.get_validator_address"></p>
<h3>pactus.wallet.get_validator_address <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.wallet.get_validator_address retrieves the validator address associated with a
public key.

<h3>Parameters</h3>
<pre>
<code>
{
 "public_key": "str" // (string) Public key for which the validator address is requested.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "address": "str" // (string) Validator address associated with the public key.
}
</pre>
<hr/>

<p id="pactus.wallet.get_new_address"></p>
<h3>pactus.wallet.get_new_address <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.wallet.get_new_address generates a new address for the specified wallet.

<h3>Parameters</h3>
<pre>
<code>
{
 "address_type": "ADDRESS_TYPE_TREASURY or
 ADDRESS_TYPE_VALIDATOR or ADDRESS_TYPE_BLS_ACCOUNT", // (string) Address type for the new address.
 "label": "str", // (string) Label for the new address.
 "wallet_name": "str" // (string) Name of the wallet for which the new address is requested.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "address_info": { // (json object) Address information.
  "address": "str", // (string)
  "label": "str", // (string)
  "path": "str", // (string)
  "public_key": "str" // (string)
 },
 "wallet_name": "str" // (string) Name of the wallet.
}
</pre>
<hr/>

<p id="pactus.wallet.get_address_history"></p>
<h3>pactus.wallet.get_address_history <span class="badge text-bg-primary fs-6 align-top">Method</span></h3>

pactus.wallet.get_address_history retrieve transaction history of an address.

<h3>Parameters</h3>
<pre>
<code>
{
 "address": "str", // (string) Address to get the transaction history of it.
 "wallet_name": "str" // (string) Name of the wallet.
}
</code>
</pre>

<h3>Result</h3>
<pre>
{
 "history_info": [ // (json array) Array of address history and activities.
  {
   "amount": n, // (numeric) amount of transaction.
   "description": "str", // (string) description of transaction.
   "payload_type": "str", // (string) payload type of transaction.
   "time": n, // (numeric) transaction timestamp.
   "transaction_id": "str" // (string) Hash of transaction.
  },
  ...
 ]
}
</pre>
<hr/>
