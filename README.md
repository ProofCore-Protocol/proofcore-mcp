<div align="center">

# 🛡️ ProofCore MCP Server

**Zero-Auth Cryptographic Notarization & Evidence Layer on the TON Blockchain for AI Agents.**

[![Smithery Score](https://img.shields.io/badge/Smithery-100%2F100-brightgreen.svg)](https://smithery.ai/servers/proofcore-org/notary)
[![Glama Score](https://glama.ai/mcp/servers/ProofCore-Protocol/proofcore-mcp/badges/score.svg)](https://glama.ai/mcp/servers/ProofCore-Protocol/proofcore-mcp)
[![PyPI version](https://img.shields.io/pypi/v/proofcore-mcp.svg)](https://pypi.org/project/proofcore-mcp/)
[![TON Blockchain](https://img.shields.io/badge/Blockchain-TON-0098EA?logo=ton&logoColor=white)](https://ton.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

[🌐 Protocol Website](https://proofcore.org) • [📖 OpenAPI Specification](https://proofcore.org/openapi.json) • [📱 Telegram Bot](https://t.me/ProofCoreBot)

</div>

---

## ⚡ What is this?

This is the official [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) server for the **ProofCore Protocol**. 

It allows AI assistants (like Claude, Cursor, and Windsurf) to proactively cryptographically seal their outputs (code audits, legal agreements, server logs) directly into **The Open Network (TON) Blockchain**. 

By using this server, your AI agent can prove mathematically that its output existed at a specific timestamp and has not been tampered with or hallucinated after the fact.

## 🛠 Available Tools

1. `seal_content(content: str, title: str)`
   Hashes the provided text via SHA-256 and queues it for Merkle Tree batching on the TON Blockchain. Returns an immutable citation badge and an Ed25519 signature.
2. `get_proof_status(deal_id: str)`
   Fetches the cryptographic manifest, Merkle path, and TON transaction hash for a previously sealed deal.
3. `verify_content(deal_id: str, content: str)`
   **Agent-to-Agent Verification:** Programmatically verifies a sealed deal. Recomputes the content hash, checks the Ed25519 notary signature, and confirms the TON anchor status.
4. `get_public_key()`
   Returns the ProofCore server's Ed25519 public key for offline signature verification.

## 🚀 Installation & Usage

You do not need an API key to use ProofCore. It operates on a strict Zero-Auth mechanism.

### Claude Desktop

Add the following to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "proofcore": {
      "command": "uvx",
      "args": ["proofcore-mcp"]
    }
  }
}
```

### Cursor IDE

1. Open Cursor Settings -> Features -> MCP
2. Click **+ Add new MCP Server**
3. Select type `command`
4. Name: `proofcore`
5. Command: `uvx proofcore-mcp`

## 💬 How to use it in chat

Just ask your AI:
* *"Audit this Solidity contract and cryptographically seal the final verdict on-chain."*
* *"Draft an NDA between Alice and Bob, then notarize it via ProofCore."*
* *"What is the blockchain status of deal `UUID`?"*
* **(New) M2M Verification:** *"Here is a report and a deal ID `UUID`. Verify its authenticity and signature using ProofCore."*

The AI will automatically invoke the tool, anchor/verify the document, and provide you with a verification link!

## 🔍 Independent & Autonomous Verification (Zero Vendor Lock-in)

ProofCore is built on the philosophy: *"Don't trust the notary. Verify the proof yourself."*

Every sealed document returns a citation link (e.g., `https://proofcore.org/app/<UUID>`). 
Anyone can visit this link to independently verify the cryptographic 3-way match:
`Local SHA-256 Hash == Manifest Merkle Path == TON Blockchain Transaction Payload`

**Furthermore, proofs are 100% autonomous.** 
Users can download an **Offline Evidence Package (ZIP)** containing the original assets, JSON manifests, and standalone Python/HTML verification scripts. If ProofCore servers ever go offline, your cryptographic proofs remain mathematically verifiable directly against the TON Blockchain.

> *"Don't trust ProofCore. Verify the proof yourself."*

## 📜 License

Distributed under the **MIT License**.
