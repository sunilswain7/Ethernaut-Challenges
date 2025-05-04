Level 5: Token

Objective:

Obtain more than 20 tokens.

Vulnerability:

Lack of underflow/overflow checks.

Explanation:

In older Solidity versions subtracting more than the balance would underflow. So we will just send 21 token so that the underflow happens which results in our balance becoming a very large number. 

Solution:

await contract.transfer("some random address", 21)

Key Takeaways:

Use SafeMath or newer Solidity versions to avoid overflows/underflows.
