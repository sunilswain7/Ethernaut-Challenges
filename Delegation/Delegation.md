Level 6: Delegation

Objective:

Claim ownership of the contract instance 

Vulnerability:

Risky use of delegatecall 

Explanation:

since delegatecall is used if we call pwn() on the Delegation contract this function will execute in Delegation's context and set its owner to msg.sender.
Solution:

web3.eth.abi.encodefunctionsignature(pwn()) 
after this you will get the fn signature 
await contract.sendTransaction({data: fn signature here})
Now when you check the owner it will be changed to your address. 

Key Takeaways:

Using delegatecall is very risky and can be also very usefull in certain scenarios but if you Rae using it be sure what are you using it for or it can be used by attackers.

