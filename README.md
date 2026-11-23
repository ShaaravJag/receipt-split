# Receipt Split

A phone-first app for splitting a restaurant or bar bill. Snap the receipt, Claude itemizes it, you tap
items to hand them to the people at the table, and it works out who owes what, with tax and tip split in
proportion to what each person ordered.

**Live app:** https://claude.ai/artifact/2rGanQW23bbgK5aeansDMF

## What it does

- **Scan a receipt.** Take a photo (or several, for a bar tab). You can crop it first, then Claude reads the
  line items, subtotal, tax, tip and total. Lines like "5 Moran's Special $60" become five $12 items you
  can hand out one at a time.
- **Paste instead.** Paste the receipt's text (for example from the iPhone's Scan Text), or the JSON Claude
  returns in a normal chat, and the items come out the same way.
- **Assign by tapping.** Pick a person from the dock at the bottom and tap their items. Share an item
  across a group or the whole table, split it by portions, or mark it comped.
- **Tax and tip done right.** Tax per receipt as an amount or a rate. Tip at 18/20/22%, a custom percent,
  a dollar amount, or the tip printed on the receipt. Both are split by what each person ordered, and the
  total is checked against the receipt.
- **Fees and discounts** split proportionally or charged to one person.
- **Settle up.** Mark who has paid you back, see what each person still owes across bills, and share the
  split as text or an image for the group chat.
- **Undo** for every change, and a history of past bills.

## How it's built

One self-contained `index.html`: Preact and htm from cdnjs, no build step.

- **Money is in integer cents.** Shared costs are split with largest-remainder rounding, so everyone's parts
  always add back to the exact total, down to the cent.
- **Local-first storage.** Every change is saved on the device first (localStorage), then synced to the
  signed-in user's own space in the Claude artifact database (`db` and `user` capabilities), with retries,
  so bills follow you across devices and still work offline.
- **Receipt reading:** uses the artifact's `sample` capability to ask Claude to read the photo or text.

## Running it

The app is built for Claude's artifact runtime, which supplies the `db`, `user` and `sample` capabilities.
Open the live link above to use it. Opened as a plain file in a browser, it still runs, but scanning with
Claude is off; manual entry and pasting Claude's JSON still work.
