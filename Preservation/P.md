 Level 16: Preservation

Objective:

Take ownership of the contract.

Vulnerability:

Already by seeing the delegatecall in this contract we should be able to know that we need to do something with this as it is not common and can be very risky to use delegate call until used in some specific cases where its recommended to use.

Solution:
```
contract MaliciousLibrary {
    address public timeZone1Library;
    address public timeZone2Library;
    address public owner;
    function setTime(uint256) public {
        owner = msg.sender;
    }
}
```
Use setFirstTime twice, first time when we call the setFirstTime funstion we pass the address of our attacking contract before pssing convert the address into uint as in settime function it requires the type of uint to be passed, then second time when we call pass anything it doesnt matter it will invoke the setime function of our attacker contract which will make us the owner of the contract 
First time we update the slot 0 in the preservation contract next we update the slot 2 which is the owner variable.
Trigger delegatecall that overwrites owner.

Key Takeaways:

delegatecall shares storage layout.
Never delegatecall to contracts you don’t fully control.

