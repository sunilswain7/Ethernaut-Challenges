# Level 19: Alien Codex

# Objective:

Claim ownership of the contract.

# Explaination:

In solidity dynamic array store their lenghth at a specific storage slot and its actual elements are stores at the keccak256 slots. Lets say that the dynamic array is stored at slot i. What this means is that the length of the array is stored in slot i and the actual elements are stored in slots starting from keccak256(p), and then the next element is stored in the next i.e keccak256(i) + 1, keccak256(i) + 2, and so on.

# Vulnerability:

In the previous versions of Solidity prior to 0.8.0, arithmetic operations on unsigned integers do not automatically check for underflows or overflows. If you decrease the length of an empty dynamic array, it underflows, setting the length to 2^256 - 1, which is the maximum value for a uint256.
The underflow effectively makes the array's length encompass the entire storage space of the contract, allowing us to access or modify any storage slot via array indexing.

# Solution:

First call  makeContact() function so that the contact flag sets to true.
Next, invoke the retract() function to underflow the codex array's length.
Next we have to calculate the index where the owner variable is sitting.
The owner variable is typically stored at slot 0. To overwrite it, you need to calculate the index in the codex array that corresponds to slot 0. Since the elements of codex start at keccak256(1), the index that maps to slot 0 is:

index = 2^256 - keccak256(1)
By writing to codex[index], you effectively write to storage slot 0, allowing you to overwrite the owner variable.

Here is the helper contract:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Exploit {
    function overwriteOwner(address targetContract, address newOwner) public {
        uint256 index = type(uint256).max - uint256(keccak256(abi.encode(uint256(1)))) + 1;
        bytes32 data = bytes32(uint256(uint160(newOwner)));
        AlienCodex(targetContract).revise(index, data);
    }
}

interface AlienCodex {
    function revise(uint256 i, bytes32 _content) external;
}
```
# Key Takeaways:

An underflow in the array means its length becomes extremely large, so large that it covers the entire storage space of the contract. This lets you access and modify any storage slot just by using an index in the array. Essentially, it's like accidentally opening access to everything in storage when you only meant to work with a specific part of it. It’s a serious issue in smart contracts because it can lead to unintended data manipulation.

