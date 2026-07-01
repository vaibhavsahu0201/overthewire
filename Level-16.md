# Bandit Level 16 → Level 17

#Objective

Find the correct SSL/TLS service running between ports `31000–32000` and submit the current password to obtain the SSH private key for the next level.

#Challenge

Unlike the previous level, the correct port was unknown. The first step was to enumerate the available services instead of trying random ports.

#Solution

```bash
nmap localhost -p 31000-32000
```

Identify the open ports and test them using:

```bash
openssl s_client -connect localhost:<port>
```

After finding the correct TLS service:

```text
<paste current password>
```

The server returns the private SSH key for `bandit17`.

#Commands Used

1. `nmap`
2. `openssl`

#Key Learning

* Finding **open ports** and identifying the **correct service** are two separate tasks.
* Every TLS service uses TCP, but not every TCP service uses TLS.
* An echo server simply returns whatever data you send.
* `openssl s_client` is useful for verifying whether a service speaks SSL/TLS.
* Messages such as `KEYUPDATE` are part of the TLS protocol and are not application errors.
* Enumeration comes before interaction—discover the service first, then choose the appropriate client.
