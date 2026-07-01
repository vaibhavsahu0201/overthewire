# Bandit Level 15 → Level 16

#Objective

Submit the current password to the service running on `localhost:30001` using SSL/TLS encryption.

#Challenge

This level introduced encrypted communication. Unlike the previous level, `nc` could not be used because the server expected a TLS connection instead of plain TCP.

#Solution

```bash
openssl s_client -connect localhost:30001
```

After the TLS handshake completes:

```text
<paste current password>
```

#Commands Used

1. `openssl`
2. `s_client`

#Key Learning

* TLS encrypts communication over TCP.
* `openssl s_client` acts as a TLS client.
* A TLS connection starts with a handshake before data can be exchanged.
* Messages like `DONE`, `KEYUPDATE`, or `RENEGOTIATING` are part of the TLS protocol and are not necessarily errors.
