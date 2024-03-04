---
tags:
  - cloud/aws
---
## Key-pairs
> Learned Key pairs can don't have to only be create when launching and instance. 
- Key-pairs consists of a private and public key. They are set of credentials that you can use to prove your identity when connecting to an Amazon EC2 instance. 
	- Amazon EC2 stores the public key and i store the private key.
	- For Linux instances, the private key allows you to securely SSH into your instance. 
	- As an alternative to key pairs, you can use [AWS Systems Manager Session Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html) to connect to your instance with an interactive one-click browser-based shell or the AWS Command Line Interface (AWS CLI).
- If you plan to connect to the instance using SSH([[Internet Protocols Suite 24-10-2023 09.37| Network Protocols]]), you must specify a key pair. 
- You can choose an existing key pair or create a new one. Depending on how you manage your security, you can specify the same key pair for all your instances or you can specify different key pairs. 
- When your instance boots for the first time, ==the public key that you specified at launch is placed on your Linux instance in an entry within `~/.ssh/authorized_keys`==
- Because Amazon EC2 doesn't keep a copy of your private key, there is no way to recover a private key if you lose it. However, there can still be a way to connect to instances for which you've lost the private key.
- You can use Amazon EC2 to create your key pairs. You can also use a third-party tool to create your key pairs, and then import the public keys to Amazon EC2.
- Amazon EC2 supports ED25519 and 2048-bit SSH-2 RSA keys for Linux instances.You can have up to 5,000 key pairs per Region.
