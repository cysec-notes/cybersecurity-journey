# Module 2: Protect organizational asset
## Overview


## Learning Objectives
- Effective data handling processes that keep information safe.
- Explore the role of encryption and hashing in safeguarding information.
- Learn about the standard access controls that companies use to authorize and authenticate users.

## Key Concepts I Learned
**Security controls** are safeguards designed to reduce specific security risks. Security controls can be organized into three types: technical, operational, and managerial.

**Information privacy** is the protection of unauthorized access and distribution of data.

A data owner is a person who decides who can access, edit, use, or destroy their information.

data custodian is anyone or anything that's responsible for the safe handling, transport, and storage of information.

Data governance is a set of processes that define how an organization manages information. Governance often includes policies that specify how to keep data private, accurate, available, and secure throughout its lifecycle.

Data governance policies commonly categorize individuals into a specific role:
1. Data owner: the person that decides who can access, edit, use, or destroy their information.
2. Data custodian: anyone or anything that's responsible for the safe handling, transport, and storage of information.
3. Data steward: the person or group that maintains and implements data governance policies set by an organization.

Information security vs. information privacy
1. Information privacy refers to the protection from unauthorized access and distribution of data.
2. Information security (InfoSec) refers to the practice of keeping data in all states away from unauthorized users.

Security assessments and audits
1. A **security audit** is a review of an organization's security controls, policies, and procedures against a set of expectations.
2. A **security assessment** is a check to determine how resilient current security implementations are against threats.

Cryptography is the process of transforming information into a form that unintended readers can't understand.
a cipher is an algorithm that encrypts information. A cryptographic key is a mechanism that decrypts ciphertext.

Public key infrastructure, or PKI, is an encryption framework that secures the exchange of information online.

Asymmetric encryption involves the use of a public and private key pair for encryption and decryption of data.

Symmetric encryption involves the use of a single secret key to exchange information.

A digital certificate is a file that verifies the identity of a public key holder.


#### Activity: Determine appropriate data handling practices
I perform this [Data leak worksheet](Data-leak-worksheet.pdf) activity, to review the results of a data risk assessment. I determine whether effective data handling processes are being implemented to protect information privacy.

#### lab: Decrypt an encrypted message
In this lab, I completed a series of tasks to obtain instructions for decrypting an encrypted file. Encryption of data in use, at rest, and in transit is critical to security functions. I use my Linux skills to uncover the clues needed to decode a classical cipher, restore a file, and reveal a hidden message.

Tasks in this lab I completed:
- List the contents of a directory

  <img width="511" height="53" alt="image" src="https://github.com/user-attachments/assets/caa346cd-b197-4aae-8d97-dccb25136d9a" />

- Read the contents of files
  <img width="917" height="102" alt="image" src="https://github.com/user-attachments/assets/a9ac5f70-0563-486b-8321-0ccdb1fb9ca6" />

The message in the .leftShift3 file appears to be scrambled. This is because the data has been encrypted using a Caesar cipher. 

- Use Linux commands to revert a classical cipher back to plaintext
  <img width="1182" height="199" alt="image" src="https://github.com/user-attachments/assets/94c10087-3176-497c-bf10-5836b988e7f5" />

- Decrypt an encrypted file and restore the file to its original state
  <img width="1901" height="100" alt="image" src="https://github.com/user-attachments/assets/e2b74ce4-94ae-44f6-bd56-4ad3095f2ee1" />

#### Personal reflection
I learn about principle of least priveledge
customers trust, users has the right how dheir data should be handled

## Next Steps
Continue Course 1 Module 2




