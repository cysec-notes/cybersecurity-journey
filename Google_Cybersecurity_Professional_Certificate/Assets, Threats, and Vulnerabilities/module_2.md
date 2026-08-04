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

#### Non-repudiation and hashing
A hash function is an algorithm that produces a code that can't be decrypted.
 non-repudiation, the concept that authenticity of information can't be denied.
 
#### The evolution of hash functions
 Salting is an additional safeguard that's used to strengthen hash functions. A salt is a random string of characters that's added to data before it's hashed. The additional characters produce a more unique hash value, making salted data resilient to rainbow table attacks.

#### Access controls and authentication systems
**Access controls**, the security controls that manage access, authorization, and accountability of information.
** Single sign-on**, or SSO, is a technology that combines several different logins into one.

Three factors of authentication: **knowledge, ownership, and characteristic**. 
HTTP uses what is known as **basic auth**, the technology used to establish a user's request to access a server.
**OAuth** is an open-standard authorization protocol that shares designated access between applications.
An API token is a small block of encrypted code that contains information about a user.

A **session** is a sequence of network HTTP basic auth requests and responses associated with the same user, like when you visit a website.
A **session ID** is a unique token that identifies a user and their device while accessing the system.
A **session cookie** is a token that websites use to validate a session and determine how long that session should last.
**Session hijacking** is an event when attackers obtain a legitimate user's session ID.
**User provisioning** is the process of creating and maintaining a user's digital identity. 

### Activity: Determine appropriate data handling practices
I perform this [Data leak worksheet](Data-leak-worksheet.pdf) activity, to review the results of a data risk assessment. I determine whether effective data handling processes are being implemented to protect information privacy.

#### lab: Decrypt an encrypted message
In this lab, I completed a series of tasks to obtain instructions for decrypting an encrypted file. Encryption of data in use, at rest, and in transit is critical to security functions. I use my Linux skills to uncover the clues needed to decode a classical cipher, restore a file, and reveal a hidden message.

**Tasks in this lab I completed:**
- List the contents of a directory

  <img width="511" height="53" alt="image" src="https://github.com/user-attachments/assets/caa346cd-b197-4aae-8d97-dccb25136d9a" />

- Read the contents of files
  <img width="917" height="102" alt="image" src="https://github.com/user-attachments/assets/a9ac5f70-0563-486b-8321-0ccdb1fb9ca6" />

The message in the .leftShift3 file appears to be scrambled. This is because the data has been encrypted using a Caesar cipher. 

- Use Linux commands to revert a classical cipher back to plaintext
  <img width="1182" height="199" alt="image" src="https://github.com/user-attachments/assets/94c10087-3176-497c-bf10-5836b988e7f5" />

- Decrypt an encrypted file and restore the file to its original state
  <img width="1901" height="100" alt="image" src="https://github.com/user-attachments/assets/e2b74ce4-94ae-44f6-bd56-4ad3095f2ee1" />

#### Activity: Create hash values
In this lab, I created and evaluated the hash values for two files. I use Linux commands to calculate the hash of two files and observe any differences in the hashes produced. Then, I determine if the files are the same, or different.

**Tasks in this lab I completed:**
- List the contents of the home directory

  <img width="452" height="94" alt="image" src="https://github.com/user-attachments/assets/c625d230-8386-4075-b673-bf1f0dd169da" />

- Compare the plain text of the two files presented for hashing
  <img width="806" height="98" alt="image" src="https://github.com/user-attachments/assets/17f12df8-7fc7-4f43-b7f1-24e596ba2805" />

  The two files appear identical when I use the cat command.

- Compute the sha256sum hash of the two separate files
  <img width="873" height="199" alt="image" src="https://github.com/user-attachments/assets/54ec8bae-c61c-4e2f-b9d2-a512fcff9c0e" />

  Now,  both files does not produce the same generated hash value.
  
- Compare the hashes provided to identify the differences
  ![Uploading image.png…]()

  The output of the cmp command indicates that the hashes differ at the first character in the first line.

#### Activity: Improve authentication, authorization, and accounting for a small business
I perform this activity, to assess the access controls used by a business. You’ll analyze their current process, identify issues, and make recommendations to improve their security practices.

#### Personal reflection
I learn about principle of least priveledge
customers trust, users has the right how dheir data should be handled

- Hash values are primarily used as a way to determine the integrity of files and applications. Hashes also keep information confidential because they can't be decrypted.

- Authorization controls are linked to the separation of duties and the principle of least privilege. Separation of duties is the principle that users should not be given levels of authorization that would allow them to misuse a system.
## Next Steps
Continue Course 1 Module 2




