# Bandit Level 24 → Level 25

## Objective

A daemon is listening on **localhost:30002**. It expects:

1. The current **Bandit24 password**.
2. A secret **4-digit PIN**.

If both are correct, it returns the password for **Bandit25**.

---

## Concepts Learned

* Brute forcing
* Bash `for` loops
* Brace expansion
* Variables
* Pipes (`|`)
* Netcat (`nc`)

---

## Solution Idea

Generate every PIN from:

```text
0000 → 9999
```

For each PIN, send:

```text
<bandit24_password> <PIN>
```

through **one single network connection**.

The challenge specifically mentions that creating a new connection for every PIN is unnecessary.

---

## Commands Learned

Generate a range:

```bash
for i in {0000..9999}
do
    echo "$i"
done
```

Pipe output into another command:

```bash
command1 | command2
```

---

## Common Mistakes

❌ Using C-style loops:

```bash
for(i=0;i<10000;i++)
```

Bash does **not** use this syntax.

---

❌ Using parentheses:

```bash
for i in (0000..9999)
```

Correct:

```bash
for i in {0000..9999}
```

---

❌ Using single quotes:

```bash
echo '$i'
```

Outputs:

```text
$i
```

Correct:

```bash
echo "$i"
```

---

❌ Sending the script itself:

```bash
cat script | nc localhost 30002
```

This sends the **contents of the script**, not the output produced by the script.

The script must be **executed**, not read with `cat`.

---

## Key Takeaways

* Bash loops are different from C loops.
* `{0000..9999}` generates a sequence using brace expansion.
* Double quotes (`"$variable"`) expand variables; single quotes (`'$variable'`) do not.
* Pipes send the **output of one command** to another command.
