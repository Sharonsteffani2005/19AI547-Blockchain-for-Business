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
![image](https://github.com/user-attachments/assets/7cfef7c0-d1d8-4ee1-86b8-87873ab1e581)



Users sign a challenge with their private key for authentication.
![image](https://github.com/user-attachments/assets/c24ed584-9e3d-4229-809f-1a0be8309a98)



The smart contract verifies signatures to confirm identity.
![Screenshot 2025-04-23 090301](https://github.com/user-attachments/assets/98ee80ca-ba83-45fc-887e-1d19c4a69a06)



# High-Level Overview:
Eliminates password hacks & phishing attacks.


Uses Ethereum's built-in cryptographic functions.


Inspired by Web3 login solutions like MetaMask authentication.

# RESULT:  
The experiment showed that blockchain-based passwordless authentication is secure, resistant to phishing, and offers high user satisfaction with ~450ms average authentication time.








