# Level14 Walkthrough

## Overview

This level has no obvious executable or script to exploit. Instead, the goal is to interact directly with the system binary `/bin/getflag` using a debugger and bypass its internal protections to retrieve the flag.

## Walkthrough

### 1. Initial inspection

```bash id="xk2s9p"
level14@SnowCrash:~$ ls -la
```

Nothing useful is present in the home directory.

Checking users:

```bash id="l3kq1c"
cat /etc/passwd
```

We see:

```bash id="9j2fva"
flag14:x:3014:3014::/home/flag/flag14:/bin/bash
```

So the target is clearly the `flag14` account.

---

### 2. Run getflag with a debugger

We use `gdb` to analyze `/bin/getflag`:

```bash id="h7dn1u"
gdb /bin/getflag
```

Run the program:

```bash id="k82sdf"
run
```

It crashes with:

```bash id="n3d82k"
Program received signal SIGSEGV, Segmentation fault.
```

---

### 3. Bypass execution flow

Instead of letting the program run normally, we manually jump to a specific instruction address:

```bash id="v9c0qe"
jump *0x08048de5
```

This skips internal checks (like UID validation or protections) and forces execution into the part of the program that prints the flag.

---

### 4. Continue execution

```bash id="z2md8w"
continue
```

Output:

```bash id="b3l9qp"
7QiHafiNa3HVozsaXkawuYrTstxbpABHD8CPnHJ
```

Even though a stack smashing warning appears afterward, the flag is already printed.

---

