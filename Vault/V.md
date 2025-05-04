Level 8: Vault

Objective:

Unlock the contract.

Vulnerability:

Private variables are not truly private in blockchain as we know everything is visible.

Explanation:

Private marked doesnt mean we cant access it it means we cant acces it just by usinf functions but it is stored in the storage which can be accessed.
Solution:

let pw = await web3.eth.getStorageAt(contract.address, 1)
await contract.unlock(pw)

Key Takeaways:

private only means inaccessible from other contracts, not hidden from the chain.
