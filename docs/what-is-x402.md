# What is x402?

The web has a status code that was reserved decades ago and barely used: **402 Payment Required**. x402 is an open standard that finally puts it to work.

## How it works

1. You (or your app, or your agent) ask a site for something: a search, a price, a gift card.
2. Instead of asking you to sign up, the site answers **402** with a price: "this costs $0.01 in USDC, paid to this address".
3. A wallet that speaks x402 signs a payment of exactly that amount and asks again, with the payment attached.
4. The site checks the payment, settles it on the blockchain, and hands over what you asked for.

No account, no API key, no subscription. You pay for the one thing you used.

## Where Fomo Spend fits

Fomo Spend is the wallet in step 3, with guardrails:

- it checks the request against **your limits** before anything is signed;
- it shows you exactly what will move and waits for your **approval**;
- it only ever pays in **USDC**, on Solana or Base.

## Words you'll see

| Word | Meaning |
| --- | --- |
| USDC | A digital dollar. 1 USDC is worth 1 US dollar. Fomo cash is USDC on Solana. |
| Solana, Base | Two blockchains where USDC lives. Fomo Spend pays on either. |
| Paid link | A URL that answers with an x402 price. |
| Facilitator | The service a seller uses to settle payments. It also covers the network fee, so you only need USDC. |
