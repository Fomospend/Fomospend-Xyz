# CLI reference

Install (Node.js 20 or newer):

```sh
npm install -g https://fomospend.xyz/fomo-spend.tgz
```

## Commands

| Command | What it does |
| --- | --- |
| `fomo-spend init` | Create the Spend account (a Solana and a Base key, encrypted with your passphrase). Adds a Base key to older accounts. |
| `fomo-spend address [--network solana\|base]` | Print the account's addresses |
| `fomo-spend fund` | Show addresses and USDC balances |
| `fomo-spend fund --from-key <base58> [--amount 10]` | Move USDC on Solana into the Spend account from a pasted key (see below) |
| `fomo-spend policy` | Show limits |
| `fomo-spend policy set --max-request 5 --max-day 20` | Set the per-payment and per-day max, in dollars |
| `fomo-spend policy allow <host>` / `deny <host>` | Add or remove an allowed site |
| `fomo-spend policy networks solana,base` | Choose networks |
| `fomo-spend pay <url> [--method POST --body '{…}' -H 'Name: value']` | Pay a URL and print the response body |
| `fomo-spend buy-card --product <slug> --value <amount>` | Buy a gift card; the code prints once |
| `fomo-spend services` | List services with a ready command for each |
| `fomo-spend ledger` | List past payments |
| `fomo-spend mcp` | Run as an MCP server (see [Agents](agents.md)) |

## Approving payments

`pay` shows the amount, asset, destination, host and what's left today, then asks `Approve? [y/N]`.

- `FOMO_SPEND_APPROVE=web` shows the same screen in your browser, served on `127.0.0.1` only while the payment is pending.
- `FOMO_SPEND_YES=1` approves automatically once your limits pass (the details are still printed).

## Funding from a pasted key

`fund --from-key` sends USDC on Solana from a key you paste (for example a Fomo trading-key export) to your Spend account. The key is used in memory for that one transfer and never written anywhere. It only accepts the pasted key text, never a file path. **Sending the full balance empties that wallet.** The source wallet needs a little SOL for the network fee.

## Environment

| Variable | Default | Use |
| --- | --- | --- |
| `FOMO_SPEND_HOME` | `~/.fomo-spend` | Where the key, limits and ledger live |
| `FOMO_SPEND_PASSPHRASE` | prompt | Unlocks the key (required for `mcp`) |
| `FOMO_SPEND_RPC_URL` | public Solana RPC | Solana RPC endpoint |
| `FOMO_SPEND_BASE_RPC_URL` | public Base RPC | Base RPC endpoint |
| `FOMO_SPEND_APPROVE` | `cli` | `cli` or `web` |
| `FOMO_SPEND_YES` | unset | `1` approves automatically after limits pass |

## Exit codes

| Code | Meaning |
| --- | --- |
| 0 | OK |
| 2 | Bad input, including a wrong passphrase |
| 3 | Network problem |
| 4 | The seller's payment request isn't something Fomo Spend can pay (not x402 v2, no USDC on Solana or Base, or the seller refused the payment) |
| 5 | Refused by your limits, or you rejected it |

## Files

| File | Contents |
| --- | --- |
| `signer.json` | Your keys, encrypted (AES-256-GCM, key derived from your passphrase with scrypt). Addresses are stored readable. |
| `policy.json` | Allowed sites, per-payment and per-day max, networks |
| `ledger.jsonl` | One line per payment, added when it's signed. Gift card codes are never written here. |
