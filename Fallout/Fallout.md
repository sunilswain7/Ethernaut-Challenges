Level 2: Fallout

Objective:

Claim ownership of the contract instance.

Concept:

Constructor naming

Explanation:

When we look at contract carefully we can catch the vulnerability in this line, function Fal1out() public payable.
-In previous solidity versions constructors were declared as functions with the same name as the contract, but here the dev mispelled Fallout as Fal1out which makes this function a normal public function which can be called by anyone and become the owwner.

Solution:

Call Fal1out() to become the owner.

Key Takeaways:

Mispelled constructor turns into a public function which can be accessed by anyone. So avoid mispelling.
