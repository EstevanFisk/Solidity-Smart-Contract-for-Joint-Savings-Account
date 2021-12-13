# Solidity-Smart-Contract-for-Joint-Savings-Account

## Overview
Creation of Solidity smart contract for joint savings account.  Specifically, a contract that accepts two user addresses that are then able to control a joint savings account. This contract was run using [Remix IDE](https://remix.ethereum.org/) with compiler 0.5.0, using deploy environment of JavaScript VM. 

## Run the Application
1. The code from the "joint_savings.sol" file must be pasted or uploaded to Remix IDE
2. Deploy using JavaScript.

## Usage

### Setup Contract
Creating initial contract consists of setting the the correct Solidity version of 0.5.0 and creating the contract "JointSavings".  All remaining functions discussed below will be added within the current contract.

````
pragma solidity ^0.5.0;

contract JointSavings {
    //insert coding here
}
````

### Define Contract Variables
These variables and their data types are specified within the contract as follows:

````
    address payable accountOne;
    address payable accountTwo;
    address public lastToWithdaw;
    uint public lastWithdrawAmount;
    uint public contractBalance;
````

### Withdraw Function
This function allows users accountOne or accountTwo to transfer funds.  Any other accounts will be given error "You don't own this account!". We also require that funds are available in the account by checking if there is enough balance to cover the amount of the withdrawl. The function also includes a setter by updating the "lastToWithdraw"

````
    function withdraw(uint amount, address payable recipient) public {

        require(recipient == accountOne || recipient == accountTwo, "You don't own this account!");

        require(contractBalance >= amount, "Insufficient funds!");


        if(lastToWithdaw != recipient){
            lastToWithdaw = recipient;
        }


        recipient.transfer(amount);

        lastWithdrawAmount = amount;

        contractBalance = address(this).balance;
    }

````
