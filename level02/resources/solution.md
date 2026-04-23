# Level02 Walkthrough

## Objective

Gain access to `flag02` and retrieve the token.

## Steps

### 1. Analyze the packet capture

* Open the `.pcap` file using Wireshark.
* Follow the TCP stream to inspect the transmitted data.

### 2. Extract the password

* The password appears with dots (`.`), which represent backspace characters.
* Apply backspaces to reconstruct the correct password:

```text
ft_waNDReL0L
```

### 3. Switch user

```bash
su flag02
```

**Password:**

```text
ft_waNDReL0L
```

### 4. Retrieve the flag

```bash
getflag
```

## Token

```text
kooda2puivaav1idi4f57q8iq
```

