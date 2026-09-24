# Gift cards

Buy gift cards for popular brands with USDC. Cards are sold and delivered by Bitrefill.

## In the app

1. Open **Gift cards** on the home page, or pick Bitrefill in the app.
2. Choose a card. Or choose **A different card?** and paste the card's link from bitrefill.com.
3. Pick an amount the card comes in (for example $25).
4. Approve the payments. A purchase takes three small steps, each shown on the approval screen:
   1. look up the card (a fraction of a cent),
   2. create the invoice (a fraction of a cent),
   3. pay for the card (the card's price).
5. Your code appears **once**. Save it right away.

## Things to know

- **Codes work like cash.** Anyone with the code can use it.
- **Purchases are final.**
- The invoice price is locked for about 15 minutes. If it expires before you approve, Fomo Spend refuses to pay and you start again.
- Fomo Spend refuses to pay if the payment asked for is different from the invoice price.
- Your limits apply: make sure your per-payment max covers the card's price.

## From the command line

```sh
fomo-spend policy allow api.bitrefill.com
fomo-spend buy-card --product amazon_com-usa --value 25
```

The code is printed once and is never written to the ledger or logs.
