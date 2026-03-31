# Basic-Account-Abstraction-EntryPoint-Mock
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract SimpleAccount {
    address public owner;

    constructor(address _owner) {
        owner = _owner;
    }

    function execute(address target, uint256 value, bytes memory data) public {
        require(msg.sender == owner, "Only owner");
        (bool success, ) = target.call{value: value}(data);
        require(success, "Execution failed");
    }

    receive() external payable {}
}
