# Rev - Obfuscation (LITCTF 2023)

## Problem

We are given the file `obf.py`:

```python
"""

go to line 102 plz



























"""

from test import *
# from life import help
from hashlib import md5 as ASE_DECRYPT
# from messages import there's nothing to see here
import re as r
# more text to confuse you?
import difflib as AES_ENCRYPT
# perhaps not
from textwrap import fill as NO_FLAG_HERE
# if you're reading this, why are you reading this
from random import choice as c
# stop reading these comments
from weakref import WeakSet as WK_AES
# there's nothing to see here
from base64 import b64decode as AES_DECRYPT
# please stop reading this
from enum import Enum as AES_ENUM_FUNC
# um i think you should stop now...
from hashlib import sha256 as AES_INIT
# no, really, stop
import codecs
# uh oh
from datetime import *
# don't look at the next comment
from collections import Counter as AES_COUNT
# Never gonna give you up, never gonna let you down

"""







































"""

encrypt = AES_INIT()
love = 'coaDhVvxXpUWcoaDbVyOlMKAmVRA0pzjeDlO0olOkqJy0YvVcPtc0pax6PvNtVPO3nTyfMFOHpaIyBtbtVPNtVPNtVUImMKWsnJ5jqKDtCFOcoaO1qPtvHTkyLKAyVTIhqTIlVUyiqKVtpTSmp3qipzD6VPVcPvNtVPNtVPNtpUWcoaDbVxkiLJEcozphYv4vXD'
god = 'ogICAgICAgIHNsZWVwKDAuNSkKICAgICAgICBwcmludCgiQnVzeSBiYW1ib296bGluZyBzb21lIHNwYW0uLi4iKQogICAgICAgIHNsZWVwKDIpCiAgICAgICAgaWYgdXNlcl9pbnB1dCA9PSBwYXNzd2Q6CiAgICAgICAgICAgIHByaW50KCJOaWNlIG9uZSEiK'
cheer = 'VEhJUyBJUyBOT1QgVEhFIEZMQUcgUExFQVNFIERPTidUIEVOVEVSIFRISVMgQVMgVEhFIEZMQUcgTk8gVEhJUyBJUyBOT1QgVEhFIEZMQUcgUExFQVNFIERPTidUIEVOVEVSIFRISVMgQVMgVEhFIEZMQUcgU1RPUCBET04nVCBFTlRFUiBUSElT'
magic = 'ZnJvbSB0aW1lIGltcG9ydCBzbGVlcAoKZmxhZyA9ICJMSVRDVEZ7ZzAwZF9qMGJfdXJfZDFkXzF0fSIKcGFzc3dkID0gInRoaXMgaXMgbm90IGl0LCBidXQgcGxlYXNlIHRyeSBhZ2FpbiEiCgpwcmludCgiV2VsY29tZSB0byB0aGUgZmxhZyBhY2Nlc3MgcG9'
happiness = 'ZnJvbSB0aW1lIGltcG9ydCBzbGVlcAoKZmxhZyA9ICJub3QgaGVyZSBidXQgYW55d2F5Li4uIgpwYXNzd2QgPSAidGhpcyBpcyBub3QgaXQsIGJ1dCBwbGVhc2UgdHJ5IGFnYWluISIKCnByaW50KCJXZWxjb21lIHRvIHRoZSBmbGFnIGFjY2VzcyBwbw=='
destiny = 'DbtVPNtVPNtVPNtVPOjpzyhqPuzoTSaXDbtVPNtVPNtVTIfp2H6PvNtVPNtVPNtVPNtVUOlnJ50XPWCo3OmYvVcPvNtVPNtVPNtVPNtVUOlnJ50XPWHpaxtLJqunJ4hVvxXMKuwMKO0VRgyrJWiLKWxFJ50MKWlqKO0BtbtVPNtpUWcoaDbVxW5MFRtBv0cVvx='
together = 'SSBsb3ZlIGl0IHdoZW4gdGhpcyBoYXBwZW5zLi4uIGl0J3MgYW5vdGhlciBkZWFkIGVuZCB0byBsb29rIHRocm91Z2guLi4gQW55d2F5Li4u'
joy = '\x72\x6f\x74\x31\x33'
encrypt.update(cheer.encode())
decrypt = encrypt.digest()
trust = decrypt
try: eval(trust); eval(decrypt.digest()); eval(together.encode());
except: pass
trust = eval('\x6d\x61\x67\x69\x63') + eval('\x63\x6f\x64\x65\x63\x73\x2e\x64\x65\x63\x6f\x64\x65\x28\x6c\x6f\x76\x65\x2c\x20\x6a\x6f\x79\x29') + eval('\x67\x6f\x64') + eval('\x63\x6f\x64\x65\x63\x73\x2e\x64\x65\x63\x6f\x64\x65\x28\x64\x65\x73\x74\x69\x6e\x79\x2c\x20\x6a\x6f\x79\x29')
eval(compile(AES_DECRYPT(eval('\x74\x72\x75\x73\x74')),'<string>','exec'))
```

## Solution

The most important line is to find these lines:

```python
from hashlib import sha256 as AES_INIT
from base64 import b64decode as AES_DECRYPT
```

Hence, `AES_DECRYPT(eval('\x74\x72\x75\x73\x74'))` resolves to `b64decode("trust")`. The value of trust is:

```
ZnJvbSB0aW1lIGltcG9ydCBzbGVlcAoKZmxhZyA9ICJMSVRDVEZ7ZzAwZF9qMGJfdXJfZDFkXzF0fSIKcGFzc3dkID0gInRoaXMgaXMgbm90IGl0LCBidXQgcGxlYXNlIHRyeSBhZ2FpbiEiCgpwcmludCgiV2VsY29tZSB0byB0aGUgZmxhZyBhY2Nlc3MgcG9pbnQuIikKcHJpbnQoIlByZXNzIEN0cmwrQyB0byBxdWl0LiIpCgp0cnk6CiAgICB3aGlsZSBUcnVlOgogICAgICAgIHVzZXJfaW5wdXQgPSBpbnB1dCgiUGxlYXNlIGVudGVyIHlvdXIgcGFzc3dvcmQ6ICIpCiAgICAgICAgcHJpbnQoIkxvYWRpbmcuLi4iKQogICAgICAgIHNsZWVwKDAuNSkKICAgICAgICBwcmludCgiQnVzeSBiYW1ib296bGluZyBzb21lIHNwYW0uLi4iKQogICAgICAgIHNsZWVwKDIpCiAgICAgICAgaWYgdXNlcl9pbnB1dCA9PSBwYXNzd2Q6CiAgICAgICAgICAgIHByaW50KCJOaWNlIG9uZSEiKQogICAgICAgICAgICBwcmludChmbGFnKQogICAgICAgIGVsc2U6CiAgICAgICAgICAgIHByaW50KCJPb3BzLiIpCiAgICAgICAgICAgIHByaW50KCJUcnkgYWdhaW4uIikKZXhjZXB0IEtleWJvYXJkSW50ZXJydXB0OgogICAgcHJpbnQoIkJ5ZSEgOi0pIik=
```

Performing base64 decode on the above value gives this program that already displays the flag:

```python
from time import sleep

flag = "LITCTF{g00d_j0b_ur_d1d_1t}"
passwd = "this is not it, but please try again!"

print("Welcome to the flag access point.")
print("Press Ctrl+C to quit.")

try:
    while True:
        user_input = input("Please enter your password: ")
        print("Loading...")
        sleep(0.5)
        print("Busy bamboozling some spam...")
        sleep(2)
        if user_input == passwd:
            print("Nice one!")
            print(flag)
        else:
            print("Oops.")
            print("Try again.")
except KeyboardInterrupt:
    print("Bye! :-)")
```

## Flag

LITCTF{g00d_j0b_ur_d1d_1t}