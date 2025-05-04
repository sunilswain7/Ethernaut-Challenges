Level 15: Naught Coin

Objective:

Drain your initial token balance despite a transfer lock.

Vulnerability:

Approval bypass using transferFrom.

Explanation:

So we know that the transfer function is locked up for 10 years and the modifier has overriden it but if we check the functions in erc20 there is a function called transferfrom and the contract clearly has not modified it which leaves us to use it to drain the initial tokens.
What we can do is that we can use the approve function to approve our address with the initial amount of token which allows us to use the transferfrom function after which we use the transferfrom function to send eth to a 3rd party address you can choose any real address and sen them the tokens.

Solution:

await contract.approve(player, initialBalance)
await contract.transferFrom(player, recipient, initialBalance)

Key Takeaways:

transfer and transferFrom can have separate logic.
Be careful to apply restrictions to all token movement functions.
