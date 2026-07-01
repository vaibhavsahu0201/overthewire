# Bandit Level 20 → Level 21

#Objective

Retrieve the password for `bandit21` by using the SetUID binary to authenticate over a local TCP connection.

#Challenge

The binary acted as a client and attempted to connect to a port specified by me. My task was to create a listening service, provide the current level's password, and receive the next password in return.

#Solution

```bash
./suconnect 5000
```

Initially returned:

```text
Could not connect
```

because nothing was listening on port `5000`.

Started a listener:

```bash
nc -l -p 5000
```

After the connection was established, I entered the current level password:

```text
<bandit20_password>
```

The service verified it and returned the password for `bandit21`.

#Commands Used

1. `ssh bandit20@bandit.labs.overthewire.org -p 2220`
2. `ls`
3. `./suconnect 5000`
4. `nc -l -p 5000`

#Key Learning

- A client cannot connect unless a server is already listening on the target port.
- `nc` can be used as a simple TCP server by running it in listening mode.
- The first connection attempt failing (`Could not connect`) helped identify that no service was waiting on the specified port.
- Reading the challenge carefully reveals which side should initiate the connection and what data needs to be exchanged.
- Understanding client-server communication is more valuable than memorizing the required commands.
