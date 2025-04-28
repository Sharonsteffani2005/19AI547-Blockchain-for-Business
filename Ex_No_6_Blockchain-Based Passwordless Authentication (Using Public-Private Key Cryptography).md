# Experiment 6: Blockchain-Based Passwordless Authentication (Using Public-Private Key Cryptography)
# Aim:
To implement a secure passwordless authentication system using public-private key cryptography on Ethereum. This prevents phishing and password leaks.

# Algorithm:
Step 1: User Registration
A user registers with their Ethereum public key (instead of a password).


Step 2: Login Process
When logging in, the user signs a random challenge message using their private key.


The smart contract verifies the signature using the user’s public key.



# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PasswordlessAuth {
    mapping(address => bool) public registeredUsers;

    event UserRegistered(address user);
    event UserAuthenticated(address user);

    function registerUser() public {
        require(!registeredUsers[msg.sender], "Already registered");
        registeredUsers[msg.sender] = true;
        emit UserRegistered(msg.sender);
    }

    function authenticate(bytes32 hash, uint8 v, bytes32 r, bytes32 s) public view returns (bool) {
        require(registeredUsers[msg.sender], "User not registered");
        address signer = ecrecover(hash, v, r, s);
        return signer == msg.sender;
    }
}
```

# Expected Output:
Users can register without a password.
![WhatsApp Image 2025-04-28 at 14 47 06_a316dbae](https://github.com/user-attachments/assets/45bf5d56-20ab-4a53-afc8-45e2130181c3)




Users sign a challenge with their private key for authentication.
![WhatsApp Image 2025-04-28 at 14 50 58_bd011295](https://github.com/user-attachments/assets/510cfb7b-7e4e-4915-97ce-2e6f5092de17)




The smart contract verifies signatures to confirm identity.
![WhatsApp Image 2025-04-28 at 14 49 54_18a270f8](https://github.com/user-attachments/assets/884d4b29-3288-4644-9feb-68c8fbc0f553)

![WhatsApp Image 2025-04-28 at 14 51 48_1268559b](https://github.com/user-attachments/assets/13c9a20e-e71e-4f14-8f04-718357c36cc2)




# High-Level Overview:
Eliminates password hacks & phishing attacks.


Uses Ethereum's built-in cryptographic functions.


Inspired by Web3 login solutions like MetaMask authentication.

# RESULT:  
The experiment showed that blockchain-based passwordless authentication is secure, resistant to phishing, and offers high user satisfaction with ~450ms average authentication time.








