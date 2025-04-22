 # REG NO : 212223110049

# DATE : 22/4/25
# Aim:
To develop a smart contract that tracks the supply chain of luxury goods, ensuring authenticity.
# Algorithm:
Step 1: The manufacturer records product creation details on-chain.

Step 2: The product moves through different supply chain checkpoints.

Step 3: The ownership of the product can be transferred securely.

Step 4: Buyers can verify the product’s authenticity.

# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract LuxurySupplyChain {
    struct Product {
        string name;
        address currentOwner;
        bool verified;
    }

    mapping(uint256 => Product) public products;

    event ProductRegistered(uint256 productId, string name);
    event OwnershipTransferred(uint256 productId, address newOwner);

    function registerProduct(uint256 productId, string memory name) public {
        require(products[productId].currentOwner == address(0), "Product already registered");
        products[productId] = Product(name, msg.sender, true);
        emit ProductRegistered(productId, name);
    }

    function transferOwnership(uint256 productId, address newOwner) public {
        require(products[productId].currentOwner == msg.sender, "Not the owner");
        products[productId].currentOwner = newOwner;
        emit OwnershipTransferred(productId, newOwner);
    }

    function verifyProduct(uint256 productId) public view returns (string memory, address, bool) {
        Product memory p = products[productId];
        return (p.name, p.currentOwner, p.verified);
    }
}
```
# EXPECTED OUTPUT:

A luxury good (e.g., a Rolex watch) is registered on-chain. 

![Screenshot 2025-04-22 120101](https://github.com/user-attachments/assets/640221ff-9555-44ae-a2fc-69faeeb48b0e)

Ownership is transferred at every checkpoint.
![Screenshot 2025-04-22 120506](https://github.com/user-attachments/assets/8dcb991f-d98a-4b8a-8a1d-2f8edd144b8b)

Buyers can check the authenticity before purchasing
![Screenshot 2025-04-22 120556](https://github.com/user-attachments/assets/a6f50888-7fbe-48e6-88ad-a5afe56a4826)

# HIGH LEVEL OVERVIEW:

Helps prevent counterfeit luxury goods.

Teaches real-world supply chain use cases.

# RESULT : 
Thus, smart contract that tracks the supply chain of luxury goods, ensuring authenticity has been created and successfully executed.
