---
title: Web3.js
actions: ['checkAnswer', 'hints']
material:
  zombieResult:
    answer: 1
---

Our Solidity contract is complete! Now we need to write a javascript frontend that interacts with the contract.

Ethereum has a javscript library called **_Web3.js_**. We'll go over in depth how to deploy a contract and how to set up Web3.js in a future lesson, but for now let's just look at some sample code for how Web3.js would interact with our deployed contract:

```
// Here's how we would access our contract:
var abi = /* abi generated by the compiler */
var ZombieFactoryContract = web3.eth.contract(abi)
var contractAddress = /* our contract address on Ethereum after deploying */
var ZombieFactory = ZombieFactoryContract.at(contractAddress)

$("button").click(function(e) {
  var name = $("#name_input").val()
  // Call our contract's `createRandomZombie()` function:
  ZombieFactory.createRandomZombie(name)
})

// Listen for the `NewZombie` event, and update the UI
var event = ZombieFactory.NewZombie(function(error, result) {
  if (error) return
  generateZombie(result.zombieId, result.name, result.dna)  
})

function generateZombie(id, name, dna) {
  let dnaStr = String(dna)
  // pad DNA with leading zeroes if it's less than 16 characters
  while (dnaStr.length < 16)
    dnaStr = "0" + dnaStr 

  // 2 digits correspond to each body part
  let zombie = {
    head: dnaStr.substring(0, 2),
    eyeType: dnaStr.substring(2, 4),
    eyeSize: dnaStr.substring(4, 6),
    shirt: dnaStr.substring(6, 8),
    legs: dnaStr.substring(8, 10),
  }

}

```

# Give it a try
