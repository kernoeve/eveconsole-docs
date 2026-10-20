# Buy Listings

A **Buy listing** turns a store round. Instead of selling to players, the store buys from them, like a buyback. The listing's [Sale Posting](../tools/sale-posting.md) holds the prices you pay. A player offers to sell, then makes an **Item Exchange** contract to you, carrying the items and asking that ISK. The offer completes when you accept the contract in game.

A store can have Sell and Buy listings side by side. Each Buy listing is a price list mail of its own and a tab of its own on the [web site](web-site.md), like any other listing. See [Listings](index.md#listings).

## Setting one up

1. **Build the price list.** Make a [Sale Posting](../tools/sale-posting.md) with the items you buy. Its **Sale Price** is what you pay, so pick a basis that suits a buyback, such as a **Specific Market** at 90 %. A Buy listing shows prices only: stock, builds, reservations and ready dates are never shown.
2. **Add the listing.** On the store's **Config ▸ General**, press **Add listing**, pick the posting and set it to **Buy**. Optionally give it a **Tab title**.
3. **Choose who receives the contracts.** **Buy contracts to** appears once the store has a Buy listing. Pick one of your characters, a corporation you poll, or the alliance of one. Sellers are told to make their contracts out to it, and each offer is matched to the contracts it receives.
4. **Optionally, say where.** Under **Buy contracts at**, search for a station or structure and pick it. The line beneath reads *Sellers are told: create all contracts at …*. Press **Clear** to stop naming one.

The settings save as you make them.

!!! warning "No one to receive contracts, no offers"

    Until **Buy contracts to** names someone, the store takes no offers, and a red line under the picker says so. A seller who tries is told the store is not taking offers at the moment.

!!! note "Corporation and alliance contracts"

    A contract made out to a corporation or alliance is seen only through a corporation login in it. Make sure such a corporation is polled, or offers will never find their contracts.

**Buy contracts at** is told, not enforced. The price list mail, the replies to offers and the web site all name the place, and an NPC station is named in the store's language. A contract made somewhere else still matches.

## How players offer

### By EVE mail

- **`PRICES`** sends each listing as its own mail. A Buy listing's mail opens by saying the store buys the items below at these prices, and that to sell, a player sends `SELL`. When the store names a place, it adds *Create all contracts at …*.
- **`SELL`** (or `OFFER`) makes an offer. The items go in the body, one per line, written as for an order:

    ```
    SELL     Archon x2
    ```

- The reply is headed *Offer … received*. It lists the items and the total, then says exactly what to do: create an **Item Exchange** contract to the store's receiver with these items in it, and the total in *I will receive*. It names the place when the store has one, and suggests putting the offer's reference in the contract's description.
- A player who drags in another character or corporation names who the contract will come from instead, such as an alt or their corporation.
- **`STATUS`** says where each offer stands: waiting for their contract, how many are on contract so far, contract received and waiting for the store, contract asking more than agreed, paid, or closed because the store declined the contract.
- **`CANCEL`** withdraws an offer that is still open.

Items written to the wrong command get a hint. An item the store sells, written in a `SELL`, is named with *send ORDER instead*, and an item it buys, written in an `ORDER`, with *send SELL instead*. A `SELL` to a store with no Buy listing is answered that the store is not buying anything at the moment. The store's usage text explains `SELL` only when the store has a Buy listing.

### On the web site

A Buy listing is a tab of its own, marked *buying*, with a **We pay** column and an **Offer** button on each row. An item without a price reads *not wanted*. Above the list, the site says who the contracts go to and, when the store names one, where to make them.

**Offer** opens **Confirm your offer**: the item, the units, the price each and the total, with what to do once the store confirms. **Send offer** sends it. The seller's **My orders** then shows the offer as *You sell*, with the contract to make (*Make an Item Exchange contract to … asking …*), and lets them withdraw it.

Tabs and Buy listings need site version **0.2.0** or later. See [Web Storefront](web-site.md#listings-on-the-site).

## Matching the contract

Every offer is booked into the [Order Tracker](../tools/order-tracker.md) as a **Buy** row, with the seller in the **Buyer** column. The app then looks for the seller's contract. A contract matches an offer when it is:

- an **Item Exchange** made out to the store's **Buy contracts to**;
- issued by the seller, by their corporation on their behalf, or by whoever they named;
- issued after the offer was made;
- carrying the item offered.

From there:

- **The price stays as quoted.** What the contract asks is recorded beside it. A contract asking more than was quoted is still linked, and flagged: **Purchase Price** turns red with a ⚠, and its tooltip gives both amounts. Check it before you accept.
- **One contract can carry a whole offer.** A contract for several items is shared over the offer's lines by what each was quoted.
- **Accepting completes it.** Once accepted contracts carry every unit, the offer is complete and the seller is paid.
- **Declining closes it.** Declining the contract cancels the offer.

Offers never take from your shelf. They reserve nothing, count toward no purchase limit, and ask the [Worklist](../tools/worklist.md) to build nothing.

## Alerts

The **Store order events** [alarm](../tools/alarms.md) speaks of offers as offers, never as orders to fill. Its headlines and spoken words cover each step:

- **New** — *New offer: … from …*, with the store and the quoted price.
- **Contracted to us** — the seller sent the contract, all of it or part of it. It asks you to accept it in game, or says that it asks more than was quoted.
- **Received** — how many of how many have come in.
- **Complete** — the contract was accepted.
- **Canceled** — the offer was withdrawn or closed.

## Notes

- Sellers must be allowed to order: the store's **who may order** rule applies to offers too.
- An offer priced well off the posting, sent from the web site, is held for you to **Book it** or **Decline**, as an order would be.
- Offers also show in the store's **Active orders**, where **Source** reads *Offer · waiting for their contract* or *Offer · their contract to accept*.
