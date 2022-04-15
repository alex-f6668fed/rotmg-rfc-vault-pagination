# Realm of the Mad God - Vault Pagination / Infinite Scrolling #

This RFC introduces a paging system to the Vault and Gift Chests located in the
player's Vault, to improve the stability and performance of the game client.

## Overview of the Problem

Currently, the Vault is a cumbersome mechanic, yet it serves one of the more
vital purposes in the game: persistence. There are not many character traits
that persist beyond death. The Vault has seen several changes throughout its
existence, and yet still manifests several growing pains that can be easily
alleviated.

To enter the Vault and see your contents, you are faced with two separate
loading spinners - first, to even enter the world. Then, to see the contents of
the Vault/Gift chest. You are then presented with a scrollable list of the chest
contents. Depending on the length of your Vault/Gift, this can begin to slow the
game. This is very apparent in Testing, where you can add an infinite number of
items by "purchasing" the free packs available.

## Proposed Solutions

The Vault/Gift chest should implement either pagination or infinite scrolling.
It would require small adjustments to the game servers and client, but would
provide a big lift in terms of quality-of-life and game performance.

### Solution 1 - Infinite Scrolling

Despite how it sounds, it's not actually that difficult a problem to solve. All
you need to know is the size of the data set (how many slots you have), how many
items per row (8), and the visual height of each row (slot and padding). With
just these three data points, you can create a "virtual" dataset representing
what is currently loaded. The scrollbar would then determine what "page" you can
see. This exact technical problem has been solved many times in web development,
and inspiration can be drawn from such solutions. Here is an excellent overview
of how infinite scrolling can work, and why it's useful:

[Infinite Scrolling in Web: Ultimate Guide by Evgenii Ray](https://evgeniiray.medium.com/infinite-scrolling-in-web-ultimate-guide-b698124b3172)

Some pros of using infinite scrolling:
- Closely matches the existing style of the Vault/Gift Chest UI
- The scroll bar would now accurately reflect the true size of the chest content
- Would have a very smooth UX with minimal UI intervention

And some cons:
- Higher complexity in implementation
- No other UI like it exists (i.e. less UI/UX continuity)

### Solution 2 - Pagination

This solution has precedence in other UI elements in game, namely the new shop,
the journal, and the Wall of Fame. It doesn't require some of the complexities
that infinite scrolling would require, at the cost of bulkier user interaction.
It simply takes more effort to change pages through button elements, but does
give the user a little more control.

Some pros of using pagination:
- Low-complexity implementation
- Has existing UI/UX precedence

And some cons:
- Heavier interaction cost than existing UI (clicking buttons vs scrolling)
- Lower overall UX than existing UI