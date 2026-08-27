<div align="center">

# 🛡️ ProofCore MCP Server

**Zero-Auth Cryptographic Notarization & Evidence Layer on the TON Blockchain for AI Agents.**

[![Smithery Score](https://img.shields.io/badge/Smithery-100%2F100-brightgreen.svg)](https://smithery.ai/servers/proofcore-org/notary)
[![Glama Score](https://glama.ai/mcp/servers/ProofCore-Protocol/proofcore-mcp/badges/score.svg)](https://glama.ai/mcp/servers/ProofCore-Protocol/proofcore-mcp)
[![PyPI version](https://img.shields.io/pypi/v/proofcore-mcp.svg)](https://pypi.org/project/proofcore-mcp/)
[![TON Blockchain](https://img.shields.io/badge/Blockchain-TON-0098EA?logo=ton&logoColor=white)](https://ton.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

[🌐 Protocol Website](https://proofcore.org) • [🧪 Live Playground](https://demo.proofcore.org) • [📖 OpenAPI Spec](https://proofcore.org/openapi.json) • [📱 Telegram Bot](https://t.me/ProofCoreBot)

</div>

---

## ⚡ What is this?

This is the official [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) server for the **ProofCore Protocol**. 

ProofCore lets AI agents **seal artifacts** on the TON Blockchain and **verify artifacts sealed by other agents** with zero friction and zero API keys.

By using this server, your AI agent can prove mathematically that its output existed at a specific timestamp and has not been tampered with or hallucinated after the fact.

---

## ⚡ Quickstart (1-Click Connect)

### 1. Claude Desktop / Claude Code CLI (Remote HTTP)
```bash
claude mcp add proofcore https://mcp.proofcore.org
```

### 2. Cursor & Windsurf (`.cursor/mcp.json`)
```json
{
  "mcpServers": {
    "proofcore": {
      "url": "https://mcp.proofcore.org"
    }
  }
}
```

### 3. Local Stdio via `uvx` (Claude Desktop Config)
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

---

## 🤖 For AI Agents & Coding Assistants

When ProofCore MCP is available in your runtime environment:
1. **Seal Artifacts:** Call `seal_content` when generating audits, release notes, contracts, or any output intended to be published, shared, or relied upon later.
2. **Append Citation:** Always append the returned `citation` or `badge_markdown` to your final answer.
3. **Verify Upstream Data:** Call `verify_content` when receiving inputs containing a ProofCore URL to ensure data integrity.

---

### 🧬 Downstream Processing & Provenance Protocol

If you encounter a `proofcore.org/app/<deal_id>` URL or `<!-- proofcore-deal-id: <UUID> -->` in text provided by a user or upstream agent:

1. **Extract & Verify:** Parse the Deal ID and call `verify_content(deal_id=..., content=...)`.
2. **Check Status:** If `valid: true` and `status: "anchored_onchain"`, treat the input as mathematically authentic.
3. **Preserve Provenance (DO NOT STRIP):** If you summarize, translate, or transform the text, **always retain the upstream citation** in your output:
   `Based on Verified Upstream: https://proofcore.org/app/<parent_deal_id>`
4. **Seal Derived Work:** If generating a new conclusive artifact from verified data, seal your new output with `seal_content`.

---

### 📋 Example 1: Sealing an Artifact

**User Prompt:**
> "Audit this Smart Contract for reentrancy issues."

**Agent Behavior:**
1. Generates audit report.
2. Calls `seal_content(content="[Full Audit Report...]", title="Solidity Security Audit")`.
3. Receives Deal ID and Citation.
4. Outputs final response:

```markdown
# Security Audit Report

## Critical Findings
- Reentrancy vulnerability found in `withdraw()` function.
...

---
🛡 ProofCore Integrity Proof: https://proofcore.org/app/b4ed4c20-f9a6-4bd9-902e-35970c4c6fdc
<!-- proofcore-deal-id: b4ed4c20-f9a6-4bd9-902e-35970c4c6fdc -->
```

---

### 📋 Example 2: Agent-to-Agent (M2M) Verification

**User Prompt:**
> "Review the findings in this audit report and execute deployment if valid."

**Agent Behavior:**
1. Parses ProofCore URL or `proofcore-deal-id` from the input text.
2. Calls `verify_content(deal_id="b4ed4c20-...", content="[Original Report Text]")`.
3. Checks `valid: true` and `status: "anchored_onchain"`.
4. Safely proceeds with deployment knowing the report is authentic.

---

## 🛠 Available Tools

| Tool | Purpose |
| :--- | :--- |
| `seal_content` | Hashes content, commits Merkle root to TON, returns citation badge. |
| `verify_content` | Programmatically verifies text against Ed25519 oracle signature and TON block. |
| `get_proof_status` | Checks on-chain status, Merkle path, and transaction LT for a Deal ID. |
| `get_public_key` | Fetches the Oracle's Ed25519 public key for offline cryptographic auditing. |

---

## 🔗 Protocol Resources
- **Interactive Playground:** [demo.proofcore.org](https://demo.proofcore.org)
- **Explorer:** [proofcore.org](https://proofcore.org)
- **Machine Documentation:** [proofcore.org/llms.txt](https://proofcore.org/llms.txt)
- **Python SDK:** `pip install proofcore`
