Vulnerability Title:
Reentrancy Vulnerability in withdraw Function

Target:
Panorama Swap Smart Contract (or any specific target related to Panorama Swap if it differs)

Severity Level:
Critical

Description:
The smart contract exposes a reentrancy vulnerability in the withdraw function. This vulnerability allows an attacker to repeatedly call the withdraw function before the contract's state (user balance) is updated. By exploiting this vulnerability, an attacker can drain the contract’s funds by calling the withdraw function recursively.

Vulnerability Details:
The withdraw function transfers Ether to the sender before updating the user's balance.
This can be exploited using a malicious contract that re-enters the withdraw function recursively, causing the contract to send Ether multiple times without updating the balance properly.Step 1: Deploy the vulnerable contract with the withdraw function.
Step 2: Deploy the MaliciousContract by passing the vulnerable contract’s address as an argument.
Step 3: Call the attack function on the malicious contract, sending 1 Ether as part of the attack.
Step 4: Observe that the contract can drain more than the intended amount by repeatedly calling withdraw.
Impact:
The reentrancy vulnerability allows attackers to drain the contract’s balance before the state is updated. This could lead to the loss of user funds and compromise the integrity of the contract. The impact of this vulnerability is critical, as it undermines trust and security in the contract’s ability to handle user funds safely.

Recommended Mitigation:
Implement the checks-effects-interactions pattern:

Update the user's balance before sending any funds.
Ensure that any external calls (e.g., Ether transfers) occur after state changes.
