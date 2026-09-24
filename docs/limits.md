# Limits

Limits are checked before anything is signed. If a payment doesn't fit, it's refused with a clear reason.

| Limit | What it does |
| --- | --- |
| Allowed sites | Only sites on this list can be paid. `*.example.com` allows subdomains. Picking a service adds its site for you, with Undo. |
| Per-payment max | No single payment can go over it. |
| Per-day max | The total for the current day (UTC) can't go over it. It counts across Solana and Base. |
| Networks | Turn Solana and/or Base on or off. |
| Asset | Always USDC. Other tokens are refused, not converted. |

First the payment request must be valid x402 (version 2). Then six checks run in this order, and the first one that fails stops the payment:

1. the site is on your allowed list
2. the network is Solana or Base mainnet, and you've allowed it
3. the asset is that network's USDC
4. the amount is within your per-payment max
5. today's total plus this amount is within your per-day max
6. the price quote is still fresh (not expired)

Limits set in the browser apply to payments from that browser. The CLI and agents keep their own limits on their own machine.
