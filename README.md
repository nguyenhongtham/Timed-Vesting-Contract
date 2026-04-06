# Timed-Vesting-Contract
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Vesting {
    address public beneficiary;
    uint256 public releaseTime;
    uint256 public amount;

    constructor(address _beneficiary, uint256 _amount) {
        beneficiary = _beneficiary;
        releaseTime = block.timestamp + 30 days; // 30 days lock
        amount = _amount;
    }

    function release() public {
        require(block.timestamp >= releaseTime, "Not yet released");
        require(msg.sender == beneficiary, "Not beneficiary");
        payable(beneficiary).transfer(amount);
    }

    receive() external payable {}
}
