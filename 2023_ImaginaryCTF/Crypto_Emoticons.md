# Crypto - Emoticons (Imaginary CTF 2023)

## Problem

We are given 2 files:

gen.py:
```python
import random

emojis = [n for n in "🌸🍔🐳🚀🌞🎉🍦🎈🐶🍕🌺🎸⚡️🦋🌼🎁"]
m = open("text.txt", "rb").read().hex()

random.shuffle(emojis)

for e, c in zip(emojis, "0123456789abcdef"):
  m = m.replace(c, e)

open("out.txt", "w").write(m)
```

out.txt:
```
🎉🌼🎈🍔🎈🌺🍕🎉🎈🐳🎈🌸🎈🌺🎈⚡🍕🌸🎁🚀🎁🐶🎈🦋🎈🚀🍕🌸🎈🌺🎁🐶🎈🎸🎈⚡🎈🌺🍕🍕🎈⚡🎁🐶🎈🦋🍕🌸🎁🐶🍕🌸🎈🍔🎈🐳🎈🚀🎈🌼🍕🐳🍕🌸🎁🚀🎁🐶🎈🦋🍕🎁🎈🌼🎁🐶🎈🍕🍕🎁🎈🦋🍕🐶🎈🌞🎈🐳🎈🌸🎈🦋🎈🚀🎁🐶🍕🎁🎈🌼🍕🐶🍕🎁🎈🌼🍕🌸🎈🌼🎈⚡🍕🎉🎈🦋🍕🎉🎈🐳🎈🌺🎈⚡🍕🌸🎁🐶🎈🌺🎈🎈🎁🐶🎈🎈🎈🦋🎈🌸🎈🐳🎈🦋🎈🚀🎁🐶🎈🌼🍕🌞🍕🐶🍕🎁🎈🌼🍕🌸🍕🌸🎈🐳🎈🌺🎈⚡🍕🌸🎁🐶🍕🌼🍕🌸🎈🌼🎈🎉🎁🐶🍕🎉🎈🌺🎁🐶🎈🌸🎈🌺🎈⚡🍕🎈🎈🌼🍕🐳🎁🐶🎈🌼🎈🍔🎈🌺🍕🎉🎈🐳🎈🌺🎈⚡🍕🌸🎁🐶🎈🌺🍕🎁🎁🐶🍕🎉🎈🌺🎈⚡🎈🌼🎁🐶🎈🐳🎈⚡🎁🐶🍕🍕🍕🎁🎈🐳🍕🎉🍕🎉🎈🌼🎈⚡🎁🐶🎈🌸🎈🌺🎈🍔🎈🍔🍕🌼🎈⚡🎈🐳🎈🌸🎈🦋🍕🎉🎈🐳🎈🌺🎈⚡🎁⚡🎁🐶🌼🎉🎈🌞🎈🌼🍕🐳🎁🐶🎈🌞🎈🦋🍕🎈🎈🌼🎁🐶🎈🎁🎈🌼🎈🌸🎈🌺🎈🍔🎈🌼🎁🐶🎈🦋🎈⚡🎁🐶🎈🐳🎈⚡🍕🎉🎈🌼🎈🍕🍕🎁🎈🦋🎈🚀🎁🐶🍕🐶🎈🦋🍕🎁🍕🎉🎁🐶🎈🌺🎈🎈🎁🐶🎈🌺🎈⚡🎈🚀🎈🐳🎈⚡🎈🌼🎁🐶🎈🍔🎈🌼🍕🌸🍕🌸🎈🦋🎈🍕🎈🐳🎈⚡🎈🍕🎁🚀🎁🐶🍕🌸🎈🌺🎈🌸🎈🐳🎈🦋🎈🚀🎁🐶🎈🍔🎈🌼🎈🎉🎈🐳🎈🦋🎁🐶🍕🐶🎈🚀🎈🦋🍕🎉🎈🎈🎈🌺🍕🎁🎈🍔🍕🌸🎁🚀🎁🐶🎈🦋🎈⚡🎈🎉🎁🐶🎈🌼🎈🍔🎈🦋🎈🐳🎈🚀🎁🐶🎈🌸🎈🌺🍕🎁🍕🎁🎈🌼🍕🌸🍕🐶🎈🌺🎈⚡🎈🎉🎈🌼🎈⚡🎈🌸🎈🌼🎁⚡🎁🐶🎉🌼🎈🍔🎈🌺🍕🎉🎈🐳🎈🌸🎈🌺🎈⚡🍕🌸🎁🐶🎈🦋🍕🎁🎈🌼🎁🐶🎈🎈🎈🌺🍕🎁🎈🍔🎈🌼🎈🎉🎁🐶🍕🌼🍕🌸🎈🐳🎈⚡🎈🍕🎁🐶🎈🦋🎁🐶🎈🌸🎈🌺🎈🍔🎈🎁🎈🐳🎈⚡🎈🦋🍕🎉🎈🐳🎈🌺🎈⚡🎁🐶🎈🌺🎈🎈🎁🐶🎈🎸🎈🌼🍕🐳🎈🎁🎈🌺🎈🦋🍕🎁🎈🎉🎁🐶🎈🌸🎈🌞🎈🦋🍕🎁🎈🦋🎈🌸🍕🎉🎈🌼🍕🎁🍕🌸🎁🐶🎈🦋🎈⚡🎈🎉🎁🐶🍕🌸🍕🐳🎈🍔🎈🎁🎈🌺🎈🚀🍕🌸🎁🚀🎁🐶🎈🦋🎈🚀🎈🚀🎈🌺🍕🍕🎈🐳🎈⚡🎈🍕🎁🐶🍕🌼🍕🌸🎈🌼🍕🎁🍕🌸🎁🐶🍕🎉🎈🌺🎁🐶🎈🌼🍕🌞🍕🐶🍕🎁🎈🌼🍕🌸🍕🌸🎁🐶🍕🎉🎈🌞🎈🌼🎈🐳🍕🎁🎁🐶🎈🎈🎈🌼🎈🌼🎈🚀🎈🐳🎈⚡🎈🍕🍕🌸🎁🐶🎈🦋🎈⚡🎈🎉🎁🐶🎈🦋🎈🎉🎈🎉🎁🐶🎈⚡🍕🌼🎈🦋🎈⚡🎈🌸🎈🌼🎁🐶🍕🎉🎈🌺🎁🐶🍕🎉🎈🌞🎈🌼🎈🐳🍕🎁🎁🐶🍕🎉🎈🌼🍕🌞🍕🎉🎁🍔🎈🎁🎈🦋🍕🌸🎈🌼🎈🎉🎁🐶🎈🌸🎈🌺🎈⚡🍕🎈🎈🌼🍕🎁🍕🌸🎈🦋🍕🎉🎈🐳🎈🌺🎈⚡🍕🌸🎁⚡🎁🐶🎈🐳🎈🌸🍕🎉🎈🎈🍕🎸🎈🎈🍕🎁🎈🌼🍕🦋🍕🌼🎈🌼🎈⚡🎈🌸🍕🐳🌼🌺🎈🦋🎈⚡🎈🦋🎈🚀🍕🐳🍕🌸🎈🐳🍕🌸🌼🌺🎈🐳🍕🌸🌼🌺🍕🎁🎈🌼🎈🦋🎈🚀🎈🚀🍕🐳🌼🌺🎈🎈🍕🌼🎈⚡🌼🌺🍕🎁🎈🐳🎈🍕🎈🌞🍕🎉🍕🍔🎁🐶🌼🎉🎈🌞🎈🌼🎁🐶🍕🐶🍕🎁🎈🐳🎈🍔🎈🦋🍕🎁🍕🐳🎁🐶🍕🐶🍕🌼🍕🎁🍕🐶🎈🌺🍕🌸🎈🌼🎁🐶🎈🌺🎈🎈🎁🐶🎈🌼🎈🍔🎈🌺🍕🎉🎈🐳🎈🌸🎈🌺🎈⚡🍕🌸🎁🐶🎈🐳🍕🌸🎁🐶🍕🎉🎈🌺🎁🐶🎈🌼🎈⚡🎈🌞🎈🦋🎈⚡🎈🌸🎈🌼🎁🐶🎈🎉🎈🐳🎈🍕🎈🐳🍕🎉🎈🦋🎈🚀🎁🐶🎈🌸🎈🌺🎈🍔🎈🍔🍕🌼🎈⚡🎈🐳🎈🌸🎈🦋🍕🎉🎈🐳🎈🌺🎈⚡🎁🐶🎈🎁🍕🐳🎁🐶🎈🎁🍕🎁🎈🐳🎈🎉🎈🍕🎈🐳🎈⚡🎈🍕🎁🐶🍕🎉🎈🌞🎈🌼🎁🐶🎈🍕🎈🦋🍕🐶🎁🐶🎈🎁🎈🌼🍕🎉🍕🍕🎈🌼🎈🌼🎈⚡🎁🐶🍕🍕🍕🎁🎈🐳🍕🎉🍕🎉🎈🌼🎈⚡🎁🐶🍕🎉🎈🌼🍕🌞🍕🎉🎁🐶🎈🦋🎈⚡🎈🎉🎁🐶🎈🎈🎈🦋🎈🌸🎈🌼🎁🍔🍕🎉🎈🌺🎁🍔🎈🎈🎈🦋🎈🌸🎈🌼🎁🐶🎈🐳🎈⚡🍕🎉🎈🌼🍕🎁🎈🦋🎈🌸🍕🎉🎈🐳🎈🌺🎈⚡🍕🌸🎁⚡🎁🐶🌼🎉🎈🌞🎈🌼🍕🐳🎁🐶🍕🐶🍕🎁🎈🌺🍕🎈🎈🐳🎈🎉🎈🌼🎁🐶🎈🦋🎁🐶🍕🍕🎈🦋🍕🐳🎁🐶🍕🎉🎈🌺🎁🐶🎈🌸🎈🌺🎈⚡🍕🎈🎈🌼🍕🐳🎁🐶🎈🌼🎈🍔🎈🌺🍕🎉🎈🐳🎈🌺🎈⚡🍕🌸🎁🚀🎁🐶🍕🌸🍕🌼🎈🌸🎈🌞🎁🐶🎈🦋🍕🌸🎁🐶🎈🌞🎈🦋🍕🐶🍕🐶🎈🐳🎈⚡🎈🌼🍕🌸🍕🌸🎁🚀🎁🐶🍕🌸🎈🦋🎈🎉🎈⚡🎈🌼🍕🌸🍕🌸🎁🚀🎁🐶🍕🌸🍕🌼🍕🎁🍕🐶🍕🎁🎈🐳🍕🌸🎈🌼🎁🚀🎁🐶🎈🌺🍕🎁🎁🐶🎈🌞🍕🌼🎈🍔🎈🌺🍕🎁🎁🚀🎁🐶🍕🍕🎈🌞🎈🐳🎈🌸🎈🌞🎁🐶🎈🌸🎈🦋🎈⚡🎁🐶🎈🎁🎈🌼🎁🐶🎈🌸🎈🌞🎈🦋🎈🚀🎈🚀🎈🌼🎈⚡🎈🍕🎈🐳🎈⚡🎈🍕🎁🐶🍕🎉🎈🌺🎁🐶🎈🌼🍕🌞🍕🐶🍕🎁🎈🌼🍕🌸🍕🌸🎁🐶🍕🌸🎈🌺🎈🚀🎈🌼🎈🚀🍕🐳🎁🐶🍕🎉🎈🌞🍕🎁🎈🌺🍕🌼🎈🍕🎈🌞🎁🐶🍕🍕🎈🌺🍕🎁🎈🎉🍕🌸🎁⚡🎁🐶🎉🎈🎈🌺🍕🎁🎁🐶🎈🌼🍕🌞🎈🦋🎈🍔🍕🐶🎈🚀🎈🌼🎁🚀🎁🐶🎈🦋🎁🐶🍕🌸🎈🐳🎈🍔🍕🐶🎈🚀🎈🌼🎁🐶🍕🌸🎈🍔🎈🐳🎈🚀🎈🌼🍕🐳🎁🐶🎈🎈🎈🦋🎈🌸🎈🌼🎁🐶🌸🍦🎁🐳🎁🐶🎈🌸🎈🦋🎈⚡🎁🐶🎈🎉🎈🌼🎈⚡🎈🌺🍕🎉🎈🌼🎁🐶🎈🌞🎈🦋🍕🐶🍕🐶🎈🐳🎈⚡🎈🌼🍕🌸🍕🌸🎁🐶🎈🌺🍕🎁🎁🐶🎈🎈🍕🎁🎈🐳🎈🌼🎈⚡🎈🎉🎈🚀🎈🐳🎈⚡🎈🌼🍕🌸🍕🌸🎁🚀🎁🐶🍕🍕🎈🌞🎈🐳🎈🚀🎈🌼🎁🐶🎈🦋🎁🐶🎈🎈🍕🎁🎈🌺🍕🍕🎈⚡🎈🐳🎈⚡🎈🍕🎁🐶🎈🎈🎈🦋🎈🌸🎈🌼🎁🐶🌸🍦🎁🌞🎁🐶🎈🌸🎈🦋🎈⚡🎁🐶🎈🐳🎈⚡🎈🎉🎈🐳🎈🌸🎈🦋🍕🎉🎈🌼🎁🐶🍕🌸🎈🦋🎈🎉🎈⚡🎈🌼🍕🌸🍕🌸🎁🐶🎈🌺🍕🎁🎁🐶🎈🎉🎈🐳🍕🌸🎈🦋🍕🐶🍕🐶🎈🌺🎈🐳🎈⚡🍕🎉🎈🍔🎈🌼🎈⚡🍕🎉🎁⚡🎁🐶🎉🌼🎈🍔🎈🌺🍕🎉🎈🐳🎈🌸🎈🌺🎈⚡🍕🌸🎁🐶🎈🌺🎈🎈🎈🎈🎈🌼🍕🎁🎁🐶🎈🦋🎁🐶🍕🎈🎈🐳🍕🌸🍕🌼🎈🦋🎈🚀🎁🐶🍕🌸🎈🌞🎈🌺🍕🎁🍕🎉🎈🌞🎈🦋🎈⚡🎈🎉🎁🐶🍕🎉🎈🌞🎈🦋🍕🎉🎁🐶🎈🌞🎈🌼🎈🚀🍕🐶🍕🌸🎁🐶🎈🌸🎈🚀🎈🦋🍕🎁🎈🐳🎈🎈🍕🐳🎁🐶🍕🎉🎈🌞🎈🌼🎁🐶🎈🐳🎈⚡🍕🎉🎈🌼🎈⚡🎈🎉🎈🌼🎈🎉🎁🐶🎈🌼🎈🍔🎈🌺🍕🎉🎈🐳🎈🌺🎈⚡🎈🦋🎈🚀🎁🐶🎈🌸🎈🌺🎈⚡🍕🎉🎈🌼🍕🌞🍕🎉🎁🐶🎈🌺🎈🎈🎁🐶🎈🦋🎁🐶🎈🍔🎈🌼🍕🌸🍕🌸🎈🦋🎈🍕🎈🌼🎁🚀🎁🐶🍕🎁🎈🌼🎈🎉🍕🌼🎈🌸🎈🐳🎈⚡🎈🍕🎁🐶🍕🎉🎈🌞🎈🌼🎁🐶🎈🌸🎈🌞🎈🦋🎈⚡🎈🌸🎈🌼🍕🌸🎁🐶🎈🌺🎈🎈🎁🐶🎈🍔🎈🐳🍕🌸🎈🌸🎈🌺🎈🍔🎈🍔🍕🌼🎈⚡🎈🐳🎈🌸🎈🦋🍕🎉🎈🐳🎈🌺🎈⚡🎁🐶🎈🌺🍕🎁🎁🐶🎈🍔🎈🐳🍕🌸🍕🌼🎈⚡🎈🎉🎈🌼🍕🎁🍕🌸🍕🎉🎈🦋🎈⚡🎈🎉🎈🐳🎈⚡🎈🍕🍕🌸🎁⚡🎁🐶🎉🍔🎈🌺🍕🎁🎈🌼🎈🌺🍕🎈🎈🌼🍕🎁🎁🚀🎁🐶🎈🌼🎈🍔🎈🌺🍕🎉🎈🐳🎈🌸🎈🌺🎈⚡🍕🌸🎁🐶🎈🦋🎈🚀🍕🌸🎈🌺🎁🐶🎈🌸🎈🌺🎈⚡🍕🎉🍕🎁🎈🐳🎈🎁🍕🌼🍕🎉🎈🌼🎁🐶🍕🎉🎈🌺🎁🐶🍕🎉🎈🌞🎈🌼🎁🐶🎈🌸🍕🎁🎈🌼🎈🦋🍕🎉🎈🐳🎈🌺🎈⚡🎁🐶🎈🌺🎈🎈🎁🐶🎈🦋🎁🐶🎈🍔🎈🌺🍕🎁🎈🌼🎁🐶🍕🐶🎈🌼🍕🎁🍕🌸🎈🌺🎈⚡🎈🦋🎈🚀🎈🐳🍕🍦🎈🌼🎈🎉🎁🐶🎈🦋🎈⚡🎈🎉🎁🐶🍕🎁🎈🌼🎈🚀🎈🦋🍕🎉🎈🦋🎈🎁🎈🚀🎈🌼🎁🐶🎈🌺🎈⚡🎈🚀🎈🐳🎈⚡🎈🌼🎁🐶🎈🌼🎈⚡🍕🎈🎈🐳🍕🎁🎈🌺🎈⚡🎈🍔🎈🌼🎈⚡🍕🎉🎁⚡🎁🐶🎉🎁🍕🐳🎁🐶🍕🌼🍕🌸🎈🐳🎈⚡🎈🍕🎁🐶🎈🌼🎈🍔🎈🌺🍕🎉🎈🐳🎈🌸🎈🌺🎈⚡🍕🌸🎁🚀🎁🐶🎈🐳🎈⚡🎈🎉🎈🐳🍕🎈🎈🐳🎈🎉🍕🌼🎈🦋🎈🚀🍕🌸🎁🐶🎈🌸🎈🦋🎈⚡🎁🐶🎈🐳🎈⚡🎈🎈🍕🌼🍕🌸🎈🌼🎁🐶🍕🎉🎈🌞🎈🌼🎈🐳🍕🎁🎁🐶🍕🍕🍕🎁🎈🐳🍕🎉🍕🎉🎈🌼🎈⚡🎁🐶🎈🍔🎈🌼🍕🌸🍕🌸🎈🦋🎈🍕🎈🌼🍕🌸🎁🐶🍕🍕🎈🐳🍕🎉🎈🌞🎁🐶🍕🐶🎈🌼🍕🎁🍕🌸🎈🌺🎈⚡🎈🦋🎈🚀🎈🐳🍕🎉🍕🐳🎁🚀🎁🐶🎈🌞🍕🌼🎈🍔🎈🌺🍕🎁🎁🚀🎁🐶🎈🌺🍕🎁🎁🐶🍕🌸🎈🦋🍕🎁🎈🌸🎈🦋🍕🌸🎈🍔🎁⚡🎁🐶🌼🎉🎈🌞🎈🐳🍕🌸🎁🐶🎈🦋🎈🎉🎈🎉🍕🌸🎁🐶🎈🎉🎈🌼🍕🐶🍕🎉🎈🌞🎁🐶🎈🦋🎈⚡🎈🎉🎁🐶🍕🎁🎈🐳🎈🌸🎈🌞🎈⚡🎈🌼🍕🌸🍕🌸🎁🐶🍕🎉🎈🌺🎁🐶🎈🌸🎈🌺🎈⚡🍕🎈🎈🌼🍕🎁🍕🌸🎈🦋🍕🎉🎈🐳🎈🌺🎈⚡🍕🌸🎁🚀🎁🐶🎈🍔🎈🦋🎈🎸🎈🐳🎈⚡🎈🍕🎁🐶🍕🎉🎈🌞🎈🌼🎈🍔🎁🐶🎈🍔🎈🌺🍕🎁🎈🌼🎁🐶🎈🌼🎈⚡🎈🍕🎈🦋🎈🍕🎈🐳🎈⚡🎈🍕🎁🐶🎈🦋🎈⚡🎈🎉🎁🐶🎈🌼🎈⚡🎈🍦🎈🌺🍕🐳🎈🦋🎈🎁🎈🚀🎈🌼🎁⚡🎁🐶🎉🌼🎈🍔🎈🌺🍕🎉🎈🐳🎈🌸🎈🌺🎈⚡🍕🌸🎁🐶🍕🌸🎈🌼🍕🎁🍕🎈🎈🌼🎁🐶🎈🦋🍕🌸🎁🐶🎈🦋🎁🐶🎈🎈🎈🌺🍕🎁🎈🍔🎁🐶🎈🌺🎈🎈🎁🐶🎈⚡🎈🌺🎈⚡🍕🎈🎈🌼🍕🎁🎈🎁🎈🦋🎈🚀🎁🐶🎈🌸🎈🌺🎈🍔🎈🍔🍕🌼🎈⚡🎈🐳🎈🌸🎈🦋🍕🎉🎈🐳🎈🌺🎈⚡🎁🐶🎈🐳🎈⚡🎁🐶🍕🎉🎈🌞🎈🌼🎁🐶🎈🎉🎈🐳🎈🍕🎈🐳🍕🎉🎈🦋🎈🚀🎁🐶🍕🎁🎈🌼🎈🦋🎈🚀🎈🍔🎁🚀🎁🐶🍕🐶🍕🎁🎈🌺🍕🎈🎈🐳🎈🎉🎈🐳🎈⚡🎈🍕🎁🐶🎈🦋🎁🐶🍕🍕🎈🦋🍕🐳🎁🐶🍕🎉🎈🌺🎁🐶🎈🌸🎈🌺🎈⚡🍕🎈🎈🌼🍕🐳🎁🐶🍕🌸🍕🌼🎈🎁🍕🎉🎈🚀🎈🌼🎁🐶🎈🌸🍕🌼🎈🌼🍕🌸🎁🐶🎈🦋🎈⚡🎈🎉🎁🐶🎈🌼🎈🍔🎈🌺🍕🎉🎈🐳🎈🌺🎈⚡🎈🦋🎈🚀🎁🐶🎈⚡🍕🌼🎈🦋🎈⚡🎈🌸🎈🌼🍕🌸🎁🐶🍕🎉🎈🌞🎈🦋🍕🎉🎁🐶🍕🍕🎈🌺🍕🌼🎈🚀🎈🎉🎁🐶🍕🎉🍕🐳🍕🐶🎈🐳🎈🌸🎈🦋🎈🚀🎈🚀🍕🐳🎁🐶🎈🎁🎈🌼🎁🐶🎈🌼🍕🌞🍕🐶🍕🎁🎈🌼🍕🌸🍕🌸🎈🌼🎈🎉🎁🐶🍕🎉🎈🌞🍕🎁🎈🌺🍕🌼🎈🍕🎈🌞🎁🐶🎈🎈🎈🦋🎈🌸🎈🐳🎈🦋🎈🚀🎁🐶🎈🌼🍕🌞🍕🐶🍕🎁🎈🌼🍕🌸🍕🌸🎈🐳🎈🌺🎈⚡🍕🌸🎁🚀🎁🐶🎈🍕🎈🌼🍕🌸🍕🎉🍕🌼🍕🎁🎈🌼🍕🌸🎁🚀🎁🐶🎈🌺🍕🎁🎁🐶🍕🎉🎈🌺🎈⚡🎈🌼🎁🐶🎈🌺🎈🎈🎁🐶🍕🎈🎈🌺🎈🐳🎈🌸🎈🌼🎁🐶🎈🐳🎈⚡🎁🐶🎈🎈🎈🦋🎈🌸🎈🌼🎁🍔🍕🎉🎈🌺🎁🍔🎈🎈🎈🦋🎈🌸🎈🌼🎁🐶🎈🐳🎈⚡🍕🎉🎈🌼🍕🎁🎈🦋🎈🌸🍕🎉🎈🐳🎈🌺🎈⚡🍕🌸🎁⚡🎁🐶🎉🐳🎈⚡🎁🐶🍕🌸🍕🌼🎈🍔🎈🍔🎈🦋🍕🎁🍕🐳🎁🚀🎁🐶🎈🌼🎈🍔🎈🌺🍕🎉🎈🐳🎈🌸🎈🌺🎈⚡🍕🌸🎁🐶🎈🦋🍕🎁🎈🌼🎁🐶🎈🍕🍕🎁🎈🦋🍕🐶🎈🌞🎈🐳🎈🌸🎈🦋🎈🚀🎁🐶🍕🎁🎈🌼🍕🐶🍕🎁🎈🌼🍕🌸🎈🌼🎈⚡🍕🎉🎈🦋🍕🎉🎈🐳🎈🌺🎈⚡🍕🌸🎁🐶🎈🌺🎈🎈🎁🐶🎈🎈🎈🦋🎈🌸🎈🐳🎈🦋🎈🚀🎁🐶🎈🌼🍕🌞🍕🐶🍕🎁🎈🌼🍕🌸🍕🌸🎈🐳🎈🌺🎈⚡🍕🌸🎁🐶🍕🎉🎈🌞🎈🦋🍕🎉🎁🐶🎈🌞🎈🦋🍕🎈🎈🌼🎁🐶🍕🎁🎈🌼🍕🎈🎈🌺🎈🚀🍕🌼🍕🎉🎈🐳🎈🌺🎈⚡🎈🐳🍕🍦🎈🌼🎈🎉🎁🐶🎈🌺🎈⚡🎈🚀🎈🐳🎈⚡🎈🌼🎁🐶🎈🌸🎈🌺🎈🍔🎈🍔🍕🌼🎈⚡🎈🐳🎈🌸🎈🦋🍕🎉🎈🐳🎈🌺🎈⚡🎁⚡🎁🐶🌼🎉🎈🌞🎈🌼🍕🐳🎁🐶🎈🦋🎈🚀🎈🚀🎈🌺🍕🍕🎁🐶🎈🐳🎈⚡🎈🎉🎈🐳🍕🎈🎈🐳🎈🎉🍕🌼🎈🦋🎈🚀🍕🌸🎁🐶🍕🎉🎈🌺🎁🐶🎈🌼🍕🌞🍕🐶🍕🎁🎈🌼🍕🌸🍕🌸🎁🐶🎈🌼🎈🍔🎈🌺🍕🎉🎈🐳🎈🌺🎈⚡🍕🌸🎁🐶🎈🦋🎈⚡🎈🎉🎁🐶🎈🦋🎈🎉🎈🎉🎁🐶🎈🌸🎈🌺🎈⚡🍕🎉🎈🌼🍕🌞🍕🎉🎁🐶🍕🎉🎈🌺🎁🐶🍕🎉🎈🌞🎈🌼🎈🐳🍕🎁🎁🐶🍕🍕🍕🎁🎈🐳🍕🎉🍕🎉🎈🌼🎈⚡🎁🐶🎈🍔🎈🌼🍕🌸🍕🌸🎈🦋🎈🍕🎈🌼🍕🌸🎁🚀🎁🐶🎈🐳🎈🍔🍕🐶🍕🎁🎈🌺🍕🎈🎈🐳🎈⚡🎈🍕🎁🐶🍕🌼🎈⚡🎈🎉🎈🌼🍕🎁🍕🌸🍕🎉🎈🦋🎈⚡🎈🎉🎈🐳🎈⚡🎈🍕🎁🐶🎈🦋🎈⚡🎈🎉🎁🐶🍕🎁🎈🌼🎈🎉🍕🌼🎈🌸🎈🐳🎈⚡🎈🍕🎁🐶🍕🎉🎈🌞🎈🌼🎁🐶🍕🎁🎈🐳🍕🌸🎈🎸🎁🐶🎈🌺🎈🎈🎁🐶🎈🍔🎈🐳🍕🌸🎈🌸🎈🌺🎈🍔🎈🍔🍕🌼🎈⚡🎈🐳🎈🌸🎈🦋🍕🎉🎈🐳🎈🌺🎈⚡🎁⚡🎁🐶🎉🎁🍕🐳🎁🐶🎈🐳🎈⚡🎈🌸🎈🌺🍕🎁🍕🐶🎈🌺🍕🎁🎈🦋🍕🎉🎈🐳🎈⚡🎈🍕🎁🐶🎈🌼🎈🍔🎈🌺🍕🎉🎈🐳🎈🌸🎈🌺🎈⚡🍕🌸🎁🐶🎈🐳🎈⚡🍕🎉🎈🌺🎁🐶🎈🎉🎈🐳🎈🍕🎈🐳🍕🎉🎈🦋🎈🚀🎁🐶🎈🌸🎈🌺🎈⚡🍕🎈🎈🌼🍕🎁🍕🌸🎈🦋🍕🎉🎈🐳🎈🌺🎈⚡🍕🌸🎁🚀🎁🐶🍕🐶🎈🌼🎈🌺🍕🐶🎈🚀🎈🌼🎁🐶🎈🌸🎈🦋🎈⚡🎁🐶🎈🐳🎈⚡🎈🎈🍕🌼🍕🌸🎈🌼🎁🐶🍕🎉🎈🌞🎈🌼🎈🐳🍕🎁🎁🐶🍕🎉🎈🌼🍕🌞🍕🎉🍕🌸🎁🐶🍕🍕🎈🐳🍕🎉🎈🌞🎁🐶🍕🐶🎈🌼🍕🎁🍕🌸🎈🌺🎈⚡🎈🦋🎈🚀🎈🐳🍕🎉🍕🐳🎁🐶🎈🦋🎈⚡🎈🎉🎁🐶🎈🌸🍕🎁🎈🌼🎈🦋🍕🎉🎈🌼🎁🐶🎈🦋🎁🐶🎈🍔🎈🌺🍕🎁🎈🌼🎁🐶🍕🎈🎈🐳🎈🎁🍕🎁🎈🦋🎈⚡🍕🎉🎁🐶🎈🦋🎈⚡🎈🎉🎁🐶🍕🎁🎈🌼🎈🚀🎈🦋🍕🎉🎈🦋🎈🎁🎈🚀🎈🌼🎁🐶🎈🌺🎈⚡🎈🚀🎈🐳🎈⚡🎈🌼🎁🐶🎈🌼🎈⚡🍕🎈🎈🐳🍕🎁🎈🌺🎈⚡🎈🍔🎈🌼🎈⚡🍕🎉🎁⚡🐶🍦
```

## Solution

Based on the code in `gen.py`, we observe that each emoji represents 1 hex character in the hexadecimal version of the ciphertext. Furthermore, we note that a substitution cipher is used, substitution 0-F with an emoji.

To make things simpler and less colorful, we first perform a frequency analysis after converting each emoji to some random characters 0-F. Results are as follows:

```
[('7', 1234), ('9', 566), ('f', 449), ('8', 323), ('e', 238), ('0', 207), ('5', 192), ('c', 176), ('2', 174), ('a', 154), ('d', 142), ('3', 84), ('1', 68), ('4', 62), ('6', 6), ('b', 5)]
```

Looking at the ascii table and assuming the plaintext is in English, we expect the frequencies of '6' and '7' to be highest since they correspond to lower-case letters. Other notable characters include `' '=x020` and '4' and '5' being the first hex character for upper-case letters. Performing some simple substitions with the help of quipquip yielded the following:

```
# Quipquip with first 200 chars, give intution to 1st word
#sub_map['7'] = '6'
#sub_map['9'] = '7'
#sub_map['6'] = '9'
#sub_map['f'] = '4'
#sub_map['e'] = '5'
#sub_map['f'] = '4'
#sub_map['8'] = '3'
't motion sld also dknown dasd smiley s l dared graphiald representations d of d fai alderpressions dt seed to donveyd emotions dordtoned in d written dom mtniation nd theyd have dheomed and integral d partd of don lined messaging ld so i ald me eiad platforms ldane de mail dorresp on een endt motions dared for meed tsing dado m hinationd of d key hoared harat ers daned sym holsld allowing dts er sd to der pressd their d feelings dane daeed ntaned tod theird ter tmha seed onversations nd it ff retenyu analysis ui su really uft nu right cd the dprimary d p trposed of demotions disd to '
``````

It would seem as though the first word is "Emoticons". This provides us with a way to reliably perform the substitution for all remaining hex characters to obtain the plaintext:

```
Emoticons, also known as smileys, are graphical representations of facial expressions used to convey emotions or tone in written communication. They have become an integral part of online messaging, social media platforms, and email correspondence. Emoticons are formed using a combination of keyboard characters and symbols, allowing users to express their feelings and add nuance to their text-based conversations. ictf{frequency_analysis_is_really_fun_right} The primary purpose of emoticons is to enhance digital communication by bridging the gap between written text and face-to-face interactions. They provide a way to convey emotions, such as happiness, sadness, surprise, or humor, which can be challenging to express solely through words. For example, a simple smiley face :) can denote happiness or friendliness, while a frowning face :( can indicate sadness or disappointment. Emoticons offer a visual shorthand that helps clarify the intended emotional context of a message, reducing the chances of miscommunication or misunderstandings. Moreover, emoticons also contribute to the creation of a more personalized and relatable online environment. By using emoticons, individuals can infuse their written messages with personality, humor, or sarcasm. This adds depth and richness to conversations, making them more engaging and enjoyable. Emoticons serve as a form of nonverbal communication in the digital realm, providing a way to convey subtle cues and emotional nuances that would typically be expressed through facial expressions, gestures, or tone of voice in face-to-face interactions. In summary, emoticons are graphical representations of facial expressions that have revolutionized online communication. They allow individuals to express emotions and add context to their written messages, improving understanding and reducing the risk of miscommunication. By incorporating emoticons into digital conversations, people can infuse their texts with personality and create a more vibrant and relatable online environment.
```

The solve script used in helping the above analysis is below:

```python
data = None
with open('out.txt', 'rb') as f:
    data = f.read()

emojis = list(map(lambda x: x.encode('utf-8'), list("🌸🍔🐳🚀🌞🎉🍦🎈🐶🍕🌺🎸⚡️🦋🌼🎁")))
emoji_translate_map = {}
ciphertext_freq_map = {}
for i in range(len(emojis)):
    # b'\xef\xb8\x8f': 0 doesn't exist after frequency analysis, remove
    if emojis[i] == b'\xef\xb8\x8f':
        continue
    emoji_translate_map[emojis[i]] = '0123456789abcdef'[len(emoji_translate_map)]
    ciphertext_freq_map[emoji_translate_map[emojis[i]]] = 0

# Frequency analysis + translation
i = 0
ciphertext = ""
while i < len(data):
    if data[i:i+3] in emoji_translate_map:
        ciphertext += emoji_translate_map[data[i:i+3]]
        ciphertext_freq_map[emoji_translate_map[data[i:i+3]]] += 1
        i += 3
    if data[i:i+4] in emoji_translate_map:
        ciphertext_freq_map[emoji_translate_map[data[i:i+4]]] += 1
        ciphertext += emoji_translate_map[data[i:i+4]]
        i += 4

ct_freq = []
for k, v in ciphertext_freq_map.items():
    ct_freq.append((k, v))
ct_freq.sort(key=lambda x: x[1])
print(ct_freq[::-1])

# Substitution cipher with some frequency analysis for letters of byte
sub_map = {}
for c in '0123456789abcdef':
    sub_map[c] = c

# Slowly figure, not that many unique bytes too....
# First few bytes might correspond to "Emoticons" based on quipquip analysis
sub_map['7'] = '6'
sub_map['9'] = '7'
sub_map['5'] = '4'
sub_map['e'] = '5'
sub_map['1'] = 'd'
sub_map['a'] = 'f'
sub_map['5'] = '4'
sub_map['2'] = '9'
sub_map['0'] = '3'
sub_map['c'] = 'e'
# Continue the rest from here via corrections
sub_map['d'] = '1'
sub_map['3'] = 'c'
sub_map['f'] = '2'
sub_map['8'] = '0'
sub_map['4'] = '8'
# Remainder
sub_map['6'] = 'a'
sub_map['b'] = 'b'


plaintext = b''
pt_bytes = ''
unique_chars = {}
for i in range(0, len(ciphertext), 2):
    pt_byte = sub_map[ciphertext[i]] + sub_map[ciphertext[i + 1]]
    pt_bytes += pt_byte + ' '
    plaintext += bytes.fromhex(pt_byte)
    if bytes.fromhex(pt_byte) not in unique_chars:
        unique_chars[bytes.fromhex(pt_byte)] = 1
    else:
        unique_chars[bytes.fromhex(pt_byte)] += 1
print(plaintext)
print(unique_chars, len(unique_chars))
```


## Flag

ictf{frequency_analysis_is_really_fun_right}