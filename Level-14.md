# Bandit Level 14 → Level 15

#Objective

Retrieve the password for `bandit15` by submitting the current password to a service running on `localhost` at port `30000`.

#Challenge

Initially, I tried passing the password as a command-line argument to `nc`. Later, I understood that `nc` first establishes a TCP connection, then waits for input through standard input (stdin).

#Solution

```bash
cat /etc/bandit_pass/bandit14

nc localhost 30000
```

After connecting:

```text
<paste current password>
```

#Commands Used

1. `cat`
2. `nc`

#Key Learning

* `localhost` refers to the current machine.
* A port identifies a specific network service running on a host.
* `nc` (Netcat) creates a TCP connection to a host and port.
* After the connection is established, input is sent through **stdin**, not as a command-line argument.
* "Connection refused" usually means no service is listening on that port.
