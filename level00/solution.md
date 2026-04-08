# Level00 Walkthrough

## Objective

Gain access to `flag00` and retrieve the token.

## Steps

### 1. Connect to the machine

```bash
ssh level00@192.168.16.128 -p 4242
```

**Password:**

```
level00
```

### 2. Find the encoded string

```bash
cat /usr/sbin/john
```

Output:

```
cdiiddwpgswtgt
```

### 3. Decode the string

* The string is encoded using a Caesar cipher.
* Decoding it gives:

```
nottoohardhere
```

### 4. Switch user

```bash
su flag00
```

**Password:**

```
nottoohardhere
```

### 5. Retrieve the flag

```bash
getflag
```

## Token

```
x24ti5gi3x0ol2eh4esiuxias
```

