---
layout: static_page
title: "Monero tools"
title-pre-kick: "Monero tools "
title-kick: "for the network "
title-post-kick: ""
kick-class: "purple-kicks"
icon: "icon_userguides"
attribution: "<!-- Icon is based on work by Freepik (http://www.freepik.com) and is licensed under Creative Commons BY 3.0 -->"
---
# simplewallet

simplewallet is the wallet software that ships with the monero tree. It is a console program,
and manages an account (while a bitcoin wallet manages both an account and the blockchain,
Monero separates these: bitmonerod handles the blockchain, and simplewallet handles the account).

This guide assumes you already have created an account, according to the other guides, and
will show how to perform various operations from the simplewallet UI.


## Checking your balance

Since the blockchain handling and the wallet are separate programs, many uses of simplewallet
need to work with the daemon. This includes looking for incoming transactions to your address.
Once you are running both simplewallet and bitmonerod, refresh the wallet's idea of the blockchain:

  refresh

This will pull blocks from the daemon the wallet did not yet see, and update your balance
to match. To see the balance without refreshing:

  balance


## Sending monero

You will need the standard address you want to send to (a long string starting with '4'), and
possibly a payment ID, if the receiving party requires one. In that latter case, that party
may instead give you an integrated address, which is both of these packed into a single address
(integrated address do not start with 4, but A).

This is the command to use when you are sending to a standard address:

  transfer 3 ADDRESS AMOUNT PAYMENTID

Replace ADDRESS with the address you wnt to sent to, AMOUNT with how many monero you want to send.
and PAYMENTID with the payment ID you were given. If the receiving party doesn't need one, just
omit it.

If you have an integrated address to send to:

  transfer 3 ADDRESS AMOUNT

The payment ID is implicit in the integrated address in that case.

The 3 above is the mixin. It's a good idea to leave it to 3, but you can increase the number if
you want to mix with more outputs. The higher the mixin, the larger the transaction, and the
higher fees needed.


## Receiving monero

If you have your own Monero address, you just need to give your standard address to someone.
Since Monero is anonymous, you won't see what address sent anything you receive. If you want to
know, you'll have to tell the sender to use a payment ID, which is an arbitrary optional tag which
gets attached to a transaction. To make life easier, you can generate an address that already
includes a random payment ID:

  integrated_address

This will generate a random payment ID, and give you the address that includes your own account
and that payment ID. If you want to select your own payment ID, you can do that too:

  integrated_address 12346780abcdef00


## Proving to a third party you paid someone

If you pay a merchant, and the merchant claims to not have received the funds, you may need
to prove to a third party you did send the funds - or even to the merchant, if it is a honest
mistake. Monero is private, so you can't just point to your transaction in the blockchain,
as you can't tell who sent it, and who received it. However, by supplying the per-transaction
private key to a party, that party can tell whether that transaction sent monero to that
particular address. Note that storing these per-transaction keys is disabled by default, and
you will have to enable it before sending, if you think you may need it:

  set store-tx-keys 1

From now on, tx keys will be saved, and you can retrieve them later for a given transaction:

  get_tx_key 1234567890123456789012345678901212345678901234567890123456789012

Pass in the transaction ID you want the key for. Remember that a payment might have been
split in more than one transaction, so you may need several keys. You can then send that key,
or these keys, to whoever you want to provide proof of your transaction, along with the
transaction id and the address you sent to. Note that this third party, if knowing your
own address, will be able to see how much change was returned to you as well.

If you are the third party (that is, someone wants to prove to you that they sent monero
to an address), then you can check this way:

  check_tx_key TXID TXKEY ADDRESS

Replace TXID, TXKEY and ADDRESS with the transaction ID, per-transaction key, and destination
address which were supplied to you, respectively. simplewallet will check that transaction
and let you know how much monero this transaction paid to the given address.


## Getting a chance to confirm/cancel payments

If you want to get a last chance confirmation when sending a payment:

  set always-confirm-transfers 1


## How to find a payment to you

If you received a payment using a particular payment ID, you can look it up:

  payments PAYMENTID

You can give more than one payment ID too.

