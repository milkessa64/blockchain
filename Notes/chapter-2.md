
# Chapter 2

## Message Calls

- send value and calldata to contracts.
- the first message call is the beginning of the transaction(EOA->contract).
- each subsequent message call is part of the same transaction (contract->contract).
Rever
- Each message contains gas, value and call data. This is listed in solidity as global variables called:
    - `msg.sender` - the sender address of the previous message call, usually 20 bytes long
    - `msg.value` - the amount of ether sent 
    - `msg.data` - calldata of the message
    - `msg.sig` - the encoding of function in the contract
- A contract has the following syntax:
```
contract X{
    address deployer; //160 bits long
    address other Contract;
}
    constructor(address _otherContract){
        deployer = msg.sender;
        otherContract = _otherContract;
    }
```
- Any function in a contract should be explicitly defined as `payable` in its [state mutability modifier](../Notes/solidity-chapter-1.md#functions)
- The `.call` syntax is `.call{ gas, value }(calldata)`

```js
contract X {
  address otherContract;

  constructor(address _otherContract) payable {
    otherContract = _otherContract;
    (bool success, )= _otherContract.call{ value: msg.value }("");
    require(success);
  }
}
```
- This stores the `msg.value` as the amount of ether sent to pay function.
- To simply receive the gas required to run the function, we use a special function called `receive()`.

**NB:** The smallest value sent in a message call is 1 wei, which is $1\over 10^{18}$ of an ether.
- Contract can destroy themselves by using the `selfdestruct` special function. This accepts addresses to send the total ether in the contract to a specifc address.

## Reverting Functions
- A contract can REVERT a call, negating all state changes.
- Each calling contract can choose to handle that success or REVERT as well.
- A REVERT still spends gas to run the contract.
- A REVERT has the following syntax:
```
function x() {
    if(condition){
        revert ;
    }
}
 Solidity Constructors
In Solidity, the constructor is a special function used for initializing the state of a contract during deployment, similar to constructors in object-oriented programming languages.

Unique Invocation:
The constructor is called only once — at the moment the contract is deployed.

Purpose:
It's typically used for setting initial values for state variables, configuring ownership, or any other setup work that should only happen once.

Syntax Example:

solidity
pragma solidity ^0.8.20;

contract MyContract {
    uint public value;

    // Constructor function
    constructor(uint initialValue) {
        value = initialValue;
    }
}

- When a smart contract performs a non-intended action, we can use `assert` to stop said action.
## Targeting Functions

Calldata( how to target functions)
   
- Solidity doesn't know about the chain its deployed on.
- if you tell solidity to call an address with calldata, it will do that.
 
