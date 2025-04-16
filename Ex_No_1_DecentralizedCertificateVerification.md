### Experiment 1: Decentralized Certificate Verification
## Aim:
  To develop a smart contract for issuing and verifying academic certificates on Ethereum, preventing forgery and ensuring authenticity.
## Algorithm:
Issuer Creates Certificate: Generate and digitally sign the certificate.

Store Hash on Blockchain: Store the certificate’s hash and metadata on a decentralized ledger.

Verifier Retrieves Hash: The verifier checks the blockchain for the certificate hash.

Compare Hashes: If the retrieved hash matches, the certificate is valid; otherwise, it's invalid or tampered.

Revalidation (Optional): Check for updates or revocations on the blockchain.

This process ensures secure, decentralized verification.

## Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;
contract CertificateVerification {
address public university;
mapping(bytes32 => bool) public certificates; // Store hashed certificates
event CertificateIssued(bytes32 indexed certHash);
constructor() {
university = msg.sender; // University deploys the contract
}
function issueCertificate(string memory studentName, string memory degree, uint256 year) public {
require(msg.sender == university, "Only university can issue certificates");
bytes32 certHash = keccak256(abi.encodePacked(studentName, degree, year));
certificates[certHash] = true;
emit CertificateIssued(certHash);
}
function verifyCertificate(string memory studentName, string memory degree, uint256 year) public view returns (bool) {
bytes32 certHash = keccak256(abi.encodePacked(studentName, degree, year));
return certificates[certHash];
}
}
```
# Expected Output:


![image](https://github.com/user-attachments/assets/c02371f3-1bd0-4157-b612-b28c0f9da42b)

Issuer Creates Certificate: Generate and digitally sign the certificate.

Store Hash on Blockchain: Store the certificate’s hash and metadata on a decentralized ledger.

Verifier Retrieves Hash: The verifier checks the blockchain for the certificate hash.

Compare Hashes: If the retrieved hash matches, the certificate is valid; otherwise, it's invalid or tampered.

Revalidation (Optional): Check for updates or revocations on the blockchain.

This process ensures secure, decentralized verification.


# Result:
The certificate is correct if its hash matches the one stored on the blockchain, and it is not revoked or expired.
