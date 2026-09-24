# Agents and MCP

Give an AI agent its own budget. The agent gets its own Spend account with its own limits, pays through the same checks as you, can't change its own limits, and never sees your wallet.

## Set it up

On the machine the agent runs on (Node.js 20 or newer):

```sh
npm install -g https://fomospend.xyz/fomo-spend.tgz
fomo-spend init                      # creates a Solana and a Base address, encrypted with a passphrase
fomo-spend policy set --max-request 1 --max-day 10
fomo-spend policy allow api.exa.ai   # each site the agent may pay
```

## Fund it

Send USDC to the address `fomo-spend init` printed. In the web app, **Agents → Fund it** sends USDC from your connected wallet in one step. Only send what you want the agent to be able to spend.

## Connect it

Fomo Spend runs as an MCP server:

```sh
claude mcp add fomo-spend --env FOMO_SPEND_PASSPHRASE=… -- fomo-spend mcp
```

or in any MCP client's config:

```json
{
  "mcpServers": {
    "fomo-spend": {
      "command": "fomo-spend",
      "args": ["mcp"],
      "env": { "FOMO_SPEND_PASSPHRASE": "…" }
    }
  }
}
```

Tools:

| Tool | What it does |
| --- | --- |
| `spend_status` | Addresses, USDC balances, allowed sites and limits, what's left today |
| `spend_services` | Services it can pay, each with a ready request |
| `spend_pay` | Pay a URL if it passes the limits (and your approval) and return the response |
| `spend_ledger` | Recent payments |

There is no tool to change limits.

## Approval

By default each `spend_pay` opens an approval page on `127.0.0.1` on that machine and waits for you. To let the agent pay on its own, still inside its limits, set `FOMO_SPEND_YES=1`.

## Without MCP

Any agent that can run a command can call `fomo-spend pay <url>`. It prints the response body and exits with `5` when a payment is refused. See the [CLI reference](cli.md).
