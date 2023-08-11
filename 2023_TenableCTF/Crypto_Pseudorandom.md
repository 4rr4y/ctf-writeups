# Crypto - PseudoRandom (Tenable CTF 2023)

## Problem

We are given the following python script:

```python
import random
import time
import datetime  
import base64

from Crypto.Cipher import AES
flag = b"find_me"
iv = b"\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0"

for i in range(0, 16-(len(flag) % 16)):
    flag += b"\0"

ts = time.time()

print("Flag Encrypted on %s" % datetime.datetime.fromtimestamp(ts).strftime('%Y-%m-%d %H:%M'))
seed = round(ts*1000)

random.seed(seed)

key = []
for i in range(0,16):
    key.append(random.randint(0,255))

key = bytearray(key)


cipher = AES.new(key, AES.MODE_CBC, iv) 
ciphertext = cipher.encrypt(flag)

print(base64.b64encode(ciphertext).decode('utf-8'))
```

Python script output: 

```
Flag Encrypted on 2023-08-02 10:27
lQbbaZbwTCzzy73Q+0sRVViU27WrwvGoOzPv66lpqOWQLSXF9M8n24PE5y4K2T6Y
```

## Solution

We observe that the timestamp is seeded via `time.time()`. Note that `time.time()` returns the number of seconds after epoch (to 6 d.p.). Hence, the seed only uses 3 d.p. worth of the value of `time.time()`. 

The output provides time resolution up to minutes. We need to bruteforce all possible seeds by trying all 60 seconds x 1000 microseconds x all timezones values until we get the flag.

A solve script is provided below:

```python
import time, random, base64
from Crypto.Cipher import AES

ts = 1690972020
found = False
for tz in range(24): # Thankfully found flag :)
    for i in range(0,61 * 1000):
        test_ts = (ts + (tz * 60 * 60)) * 1000 + i
        seed = round(test_ts)
        random.seed(seed)
        key = []
        for i in range(0,16):
            key.append(random.randint(0,255))
        key = bytearray(key)
        ciphertext = base64.b64decode('lQbbaZbwTCzzy73Q+0sRVViU27WrwvGoOzPv66lpqOWQLSXF9M8n24PE5y4K2T6Y')
        cipher = AES.new(key, AES.MODE_CBC, b"\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0") 
        plaintext = cipher.decrypt(ciphertext)
        if b'\x00' == plaintext[-1] or b'flag' in plaintext:
            print(test_ts, plaintext)
            found = True
            break
    if found:
        break
```

Script output:
```
1690986434439 b'flag{r3411y_R4nd0m_15_R3ally_iMp0r7ant}\x00\x00\x00\x00\x00\x00\x00\x00\x00'
```

## Flag

flag{r3411y_R4nd0m_15_R3ally_iMp0r7ant}
