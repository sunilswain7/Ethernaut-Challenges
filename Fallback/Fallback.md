Level 1: Fallback

Objective:

Become the owner of the conrtract and drain its funds

Concept:

Fallback() function
recieve() function
msg.value, msg.sender

Explanation:

This contract uses the receive() function to change ownership when you send ether directly to the contract and you have some contribution already. This means you can become the owner without needing to contibute large amount of ether.

Solution:

-First call contribute() with less than 0.001 eth.
-Then send eth directly to the contract using contract.sendTransaction({from: player, value: small amt})
-This triggers the receive() function which makes you the new owner
-Call withdraw() as you are the new owner and drain the contract balance.

Key Takeaways:

Never give critcal access like ownership in a fallback/recieve function as it can be exploited if access control is weak.
