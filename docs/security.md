# Security

## What Fomo Spend never does

- Sign a payment that fails your limits.
- Sign without your approval (unless you turn on automatic approval for an agent).
- Pay in anything other than USDC, or on networks other than Solana and Base mainnet.
- Sign token approvals. On Base it only signs a one-time authorization for the exact amount.
- Touch your Fomo trading account.
- See your keys in the web app. Your wallet signs; the site only forwards requests and reads public balances.

## Where keys live

- **Web app:** in your own wallet (Phantom, MetaMask, …) or, if you sign in with email or Google, in a wallet created and secured by Privy. Fomo Spend's servers never hold them.
- **CLI and agents:** on that machine, in `~/.fomo-spend/signer.json`, encrypted with your passphrase. The key is only unlocked for a payment you've approved.

## What the site's server does

The browser can't read x402 price headers from other sites directly, so the site forwards those requests for you. It:

- only forwards to public `https://` addresses (never private or internal networks);
- only reads public blockchain data for balances;
- never receives a key, and never sends transactions on your behalf.

## Gift card codes

Codes are shown once and never saved by Fomo Spend. Treat them like cash.

## Reporting a problem

If you think you've found a security issue, please open a private report through this repository's **Security** tab rather than a public issue.
