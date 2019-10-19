# Key Management Service (KMS)

- KMS is a management service for you encrpytion keys
- Keys are regional
  - To encrpyt/decrypt data in eu-west-1, the key must belong to eu-west-1
- KMS is multi-tenant (CloudHSM is dedicated hardware. S3 Encryption and Client-Side encryption are not Key Management Solutions)

**Customer Master Key:**

- CANNOT be exported
- Customer Master Key consists of:
  - alias: name
  - creation date
  - description
  - key state: enabled, disabled, pending import, pending deletion, unavailable
  - key matarial: either customer provided or AWS provided

**Setting up a Key:**

- Create Alias
- Create Description
- Choose material option
- Define Key Administrative Permissions
  - IAM users/roles that can administer (but not use) the key through the KMS API
- Define Key Usage Permissions
  - IAM users/roles that can use the key to encrpyt and decrypt data

**API calls:**

- Encrypt: Takes in a file > encrypts it > creates a new encrypted file
- Decrypt: Takes in an encrypted file > decrypts it > creates a new decrypted file
- Re-encrypt: Takes in an encrypted file > decrypts it > re-encrypts it > immediately destroys the plain decrypted file without exposing it to the client
- Enable Key Rotation: Enables Key Rotation

**Envelope Encryption:**

Basically using a (Customer) Master Key to encrypt the key we use to encrypt data

- The Envelope KEY is used to encrypt/decrypt data
- The Customer Master Key is used to encrypt/decrypt the Envelope Key
- Before encrypt/decrypt data with the EK, the EK must first be decrypted using the CMK into a plain key
