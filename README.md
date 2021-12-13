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
    address public lastToWithrdaw;
    uint public lastWithdrawAmount;
    uint public contractBalance;
````

### Creating Setter Function for Two Accounts
Setting variables to specific account numbers of joint owners:

````
    function setAccounts(address payable account1, address payable account2) public{

        // Set the values of `accountOne` and `accountTwo` to `account1` and `account2` respectively.
        accountOne = account1;
        accountTwo = account2;
    }
````


### Withdraw Function
This function allows users accountOne or accountTwo to transfer funds.  Any other accounts will be given error "You don't own this account!". We also require that funds are available in the account by checking if there is enough balance to cover the amount of the withdrawl. The function also includes a setter by updating the "lastToWithdraw". Finally we commit thetransaction by using the "transfer" function, set the lastWithdrawAmount, and get the current contract balance after the transaction.

````
    function withdraw(uint amount, address payable recipient) public {

        require(recipient == accountOne || recipient == accountTwo, "You don't own this account!");

        require(contractBalance >= amount, "Insufficient funds!");


        if(lastToWithdraw != recipient){
            lastToWithdraw = recipient;
        }


        recipient.transfer(amount);

        lastWithdrawAmount = amount;

        contractBalance = address(this).balance;
    }

````

### Deposit Function
Note the deposit function utilizes the Remix value section to input deposit amounts. This is due to the "payable" keyword used in the deposit function scope.

````
    function deposit() public payable {

        contractBalance = address(this).balance;
    }
````

### Catch All "Fallback" Function
Sometimes it is a good idea to add a fallback function to catch deposits that do not match functions within your contract. It is the "external" and "payable" used together that make it act as a fallback for depositing into the account in particular. 

````
   function() external payable{}
````

## Examples
See example screenshots of function testing in the "Execution_Results" folder embeded in the repository. This includes testing the setAccounts function, running three deposit tests, and two withdraw tests to show full functionality.

Enjoy your coding experience!!!
