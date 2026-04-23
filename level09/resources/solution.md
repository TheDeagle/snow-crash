# Level09

## Overview

This level involves decoding an obfuscated string where each character has been shifted based on its position. By reversing the transformation, we can recover the original password.

## Walkthrough

### 1. Retrieve the encoded token

```bash id="a7k2qp"
cat token
```

Output:

```text id="b3v9ls"
f4kmm6p|=pnDBDu{
```

### 2. Decode the string

The encoding subtracts the index of each character from its ASCII value. Reverse it using Python:

```python id="c8x1rt"
s = "f4kmm6p|=\x7fpnDBDu{\x7f"
print("".join(chr(ord(c) - i) for i, c in enumerate(s)))
```

Result:

```text id="d5k4ws"
f3iji1ju5yuevaus41q1afiuq
```

### 3. Switch user

```bash id="e2p8zu"
su flag09
```

**Password:**

```text id="f9m3qx"
f3iji1ju5yuevaus41q1afiuq
```

### 4. Retrieve the flag

```bash id="g6t1yn"
getflag
```

## Token

```text id="h4r7vd"
s5cAJpM8ev6XHw998pRWG728z
```

