# Level13 Walkthrough

## Overview

This level is about bypassing a UID check in a setuid binary and understanding a custom “encryption” function. The binary only reveals the token if executed with a specific UID, but we can reverse the embedded function to recover it manually.

## Walkthrough

### 1. Inspect the binary

```bash
level13@SnowCrash:~$ ls -l
level13

level13@SnowCrash:~$ file level13
setuid ELF 32-bit executable
```

The binary is setuid and checks the current user ID before proceeding.

### 2. Analyze the main function

```c
if (getuid() != 0x1092) {
    printf("UID %d started us but we we expect %d\n", getuid(), 0x1092);
    exit(1);
}
```

* The program only runs if UID == `0x1092` (4242 in decimal)
* Otherwise, it exits immediately

If the check passes, it calls:

```c
ft_des("boe]!ai0FB@.:|L6l@A?>qJ}I");
```

### 3. Reverse the ft_des function

The function is not real DES — it’s a custom transformation:

* Iterates over each character
* Uses `"0123456"` as a repeating shift pattern
* Even index → decrement character
* Odd index → increment character
* Wraps around ASCII limits (`0x1f` → `~`, `0x7f` → space)

### 4. Reimplement the function

Instead of bypassing the UID check, we replicate the logic in our own program:

```c
char *ft_des(const char *input)
{
    char *out = strdup(input);
    int i = 0, j = 0;

    while (out[i]) {
        int shift = "0123456"[j];

        if (i % 2 == 0) {
            for (int k = 0; k < shift; k++) {
                out[i]--;
                if (out[i] == 0x1f)
                    out[i] = '~';
            }
        } else {
            for (int k = 0; k < shift; k++) {
                out[i]++;
                if (out[i] == 0x7f)
                    out[i] = ' ';
            }
        }

        i++;
        j = (j + 1) % 6;
    }

    return out;
}
```

### 5. Compile and run

```bash
gcc file.c
./a.out
```

### 6. Retrieve the token

```bash
Encrypted token: 2A31L79asukciNyi8uppkEuSx
```


