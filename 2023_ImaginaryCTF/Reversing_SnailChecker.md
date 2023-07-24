# Reversing - SnailChecker (Imaginary CTF 2023)

## Problem

We are given the following flag checker:

```python
#!/usr/bin/env python3

def enc(b):
 a = [n for n in range(b[0]*2**24+b[1]*2**16+b[2]*2**8+b[3]+1)][1:]
 c,i = 0,0
 while len([n for n in a if n != 0]) > 1:
  i%=len(a)
  if (a[i]!=0 and c==1):
   a[i],c=0,0
  if (a[i] != 0):
   c+=1
  i += 1
 return sum(a)

print(r"""
    .----.   @   @
   / .-"-.`.  \v/
   | | '\ \ \_/ )
 ,-\ `-.' /.'  /
'---`----'----'
""")
flag = input("Enter flag here: ").encode()
out = b''
for n in [flag[i:i+4] for i in range(0,len(flag),4)]:
  out += bytes.fromhex(hex(enc(n[::-1]))[2:].zfill(8))

if out == b'L\xe8\xc6\xd2f\xde\xd4\xf6j\xd0\xe0\xcad\xe0\xbe\xe6J\xd8\xc4\xde`\xe6\xbe\xda>\xc8\xca\xca^\xde\xde\xc4^\xde\xde\xdez\xe8\xe6\xde':
 print("[*] Flag correct!")
else:
 print("[*] Flag incorrect.")
```

## Solution

The "snail" part is the `enc()` method. Observe that the flag is broken into blocks of 4 bytes (labelled `K` for convenience), and values [1..K] are stored in `a`. After which, values in [1..K] are eliminated in alternate fashion (skipping numbers already eliminated), and the last un-eliminated value is returned.

This reminds us of the Josephus problem (`n` people stand in a circle, kill every `k`-th person until last person stands). For the specific case of `k=2` as per this problem, we have a fast [solution](https://www.geeksforgeeks.org/josephus-problem-when-k-is-2/):

```
# Faster version for k=2 specifically
def josephus_v2(n):
    # Return 2n - 2^(1 + floor(Logn)) + 1
    p = 1
    while p <= n:
        p *= 2
    return (2 * n) - p + 1
```

For this problem, instead of being given `n` and `k`, we are given the "last person(value) standing" and `k`, and we need to find `n`. We can therefore reverse the logic of `josephus_v2` above to find `n`. Doing this (`inverse_josephus_v2()` below) for every 4 bytes of the obfuscated flag gives us the flag via this solve script:

```python
def inverse_josephus_v2(k):
  '''
  k = 2n - 2^(1 + floor(log2(n))) + 1
  (k - 1)/2 = n - 2^(floor(log2(n)))
  Compute highest power of 2 and try solve for n
  '''
  k = k / 2
  result = None
  for i in range(64):
    if ((1 << i) > k):
      result = hex(int((1 << i) + k))
      break
  return bytes.fromhex(result[2:])[::-1]
    

def p32(v):
  return v[0] * (1 << 24) + v[1] * (1 << 16) + v[2] * (1 << 8) + v[3]

def solve():
  out = b'L\xe8\xc6\xd2f\xde\xd4\xf6j\xd0\xe0\xcad\xe0\xbe\xe6J\xd8\xc4\xde`\xe6\xbe\xda>\xc8\xca\xca^\xde\xde\xc4^\xde\xde\xdez\xe8\xe6\xde'
  flag = b''
  for i in range(0, len(out), 4):
    n = out[i:i + 4]
    result = inverse_josephus_v2(p32(n))
    flag += result
  print(flag)
  # ictf{josephus_problem_speed?boooooooost} somehow gives '?' perhaps due to some rounding error?
  # After correction: ictf{josephus_problem_speed_boooooooost}

solve()
```

## Flag

ictf{josephus_problem_speed_boooooooost}
