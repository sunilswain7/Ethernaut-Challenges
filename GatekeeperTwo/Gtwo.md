Level 14: Gatekeeper Two

Objective:

Pass three new gates based on bit operations and code size.

Explanation:

Gate 1: Using a helper contract to interact with the contract

Gate 2: extcodesize(msg.sender) == 0 only works in constructor

Gate 3: Use the xor propert of a^b=c then a^c=b and manipulate the code.

🛠️ Solution:

contract Hack {
    constructor() {
        GatekeeperTwo gatekc = GatekeeperTwo(gatekeeper contracts address);
        bytes8 key = bytes8(uint64(bytes8(keccak256(abi.encodePacked(address(this))))) ^ type(uint64).max);
        gatekc.enter(key);
    }
}


Key Takeaways:

Code size is 0 during construction.

Use of XOR and typecasting.
