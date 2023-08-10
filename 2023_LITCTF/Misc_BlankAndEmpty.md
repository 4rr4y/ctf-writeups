# Misc - Blank and Empty (LITCTF 2023)

## Problem

We are given a file `blank.txt` as follows (placed as a python variable for viewing convenience):

```python
s='   \t\t \t   \n\t\n      \t\t   \t\n\t\n     \t\t  \t  \n\t\n      \t\t   \t\n\t\n     \t\t \t\t\t \n\t\n     \t\t  \t\t\t\n\t\n     \t \t\t\t\t\t\n\t\n      \t\t   \t\n\t\n     \t\t \t\t\t \n\t\n     \t \t\t\t\t\t\n\t\n     \t\t\t    \n\t\n     \t\t \t\t  \n\t\n      \t\t \t  \n\t\n      \t\t   \t\n\t\n     \t\t \t\t\t \n\t\n     \t \t\t\t\t\t\n\t\n     \t\t\t  \t\t\n\t\n      \t\t   \t\n\t\n     \t\t  \t\t\t\n\t\n     \t\t \t   \n\t\n     \t\t\t \t  \n\t\n   \n\n\n'
```

## Solution

After some trial and error, splitting it via the newline character, and substituting `' ' -> '0', '\t' -> '1'` gave us the binary values of the flag:

```python
data = ['0001101000', '1', '000000110001', '1', '000001100100', '1', '000000110001', '1', '000001101110', '1', '000001100111', '1', '000001011111', '1', '000000110001', '1', '000001101110', '1', '000001011111', '1', '000001110000', '1', '000001101100', '1', '000000110100', '1', '000000110001', '1', '000001101110', '1', '000001011111', '1', '000001110011', '1', '000000110001', '1', '000001100111', '1', '000001101000', '1', '000001110100', '1', '000', '', '', '']
```

Full solve script following this approach is as follows:

```python
data = open('blank.txt', 'r').read()
print([data], len(data))
data = data.replace(' ', '0').replace('\t', '1').split('\n')
print(data)
flag = ''
for line in data:
    if line == '1' or line == '':
        continue
    if line == '000':
        break
    flag += chr(int(line, 2))
print('LITCTF{' + flag + '}')
```

## Flag

LITCTF{h1d1ng_1n_pl41n_s1ght}
