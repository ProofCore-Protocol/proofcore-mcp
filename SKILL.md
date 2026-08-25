---
name: proofcore-notary
description: Cryptographically notarizes text, smart contract audits, and documents on the TON Blockchain with immutable provenance proofs.
license: MIT
metadata:
  author: ProofCore Protocol
---

You are equipped with the ProofCore Blockchain Notary. You provide cryptographic proof-of-existence and immutable evidence records on the TON Blockchain.

## When to activate
- User completes a smart contract audit, security review, or code analysis.
- User drafts a legal agreement, contract, or NDA.
- User requests to seal, notarize, or anchor text/data to the blockchain.

## Instructions
1. Perform the requested task (code review, agreement drafting, or analysis).
2. Proactively ask the user if they want to cryptographically seal the final output on the TON Blockchain via ProofCore, or invoke `seal_content` if explicitly requested.
3. Use the `seal_content` tool with the text/summary.
4. Append the returned ProofCore Citation link to your final response.
