# Web - Perfect Picture (Imaginary CTF 2023)

## Problem

We are provided with app.py:

```python
from flask import Flask, render_template, request
from PIL import Image
import exiftool
import random
import os

app = Flask(__name__)
app.debug = False

os.system("mkdir /dev/shm/uploads/")
app.config['UPLOAD_FOLDER'] = '/dev/shm/uploads/'
app.config['ALLOWED_EXTENSIONS'] = {'png'}

def check(uploaded_image):
    with open('flag.txt', 'r') as f:
        flag = f.read()
    with Image.open(app.config['UPLOAD_FOLDER'] + uploaded_image) as image:
        w, h = image.size
        if w != 690 or h != 420:
            return 0
        if image.getpixel((412, 309)) != (52, 146, 235, 123):
            return 0
        if image.getpixel((12, 209)) != (42, 16, 125, 231):
            return 0
        if image.getpixel((264, 143)) != (122, 136, 25, 213):
            return 0

    with exiftool.ExifToolHelper() as et:
        metadata = et.get_metadata(app.config['UPLOAD_FOLDER'] + uploaded_image)[0]
        try:
            if metadata["PNG:Description"] != "jctf{not_the_flag}":
                return 0
            if metadata["PNG:Title"] != "kool_pic":
                return 0
            if metadata["PNG:Author"] != "anon":
                return 0
        except:
            return 0
    return flag

def allowed_file(filename):
    return '.' in filename and filename.rsplit('.', 1)[1].lower() in app.config['ALLOWED_EXTENSIONS']

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/upload', methods=['POST'])
def upload():
    if 'file' not in request.files:
        return 'no file selected'

    file = request.files['file']

    if file.filename == '':
        return 'no file selected'

    if file and allowed_file(file.filename):
        filename = file.filename

        img_name = f'{str(random.randint(10000, 99999))}.png'
        file.save(app.config['UPLOAD_FOLDER'] + img_name)
        res = check(img_name)

        if res == 0:
            os.remove(app.config['UPLOAD_FOLDER'] + img_name)
            return("hmmph. that image didn't seem to be good enough.")
        else:
            os.remove(app.config['UPLOAD_FOLDER'] + img_name)
            return("now that's the perfect picture:<br>" + res)

    return 'invalid file'

if __name__ == '__main__':
    app.run()
```

A template file for UI is also provided:
```html
<!DOCTYPE html>
<html>
<head>
    <title>File Upload</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
</head>
<body>
    <form action="/upload" method="post" enctype="multipart/form-data">
        <label for="file">Select a file to upload:</label>
        <input type="file" id="file" name="file" accept=".jpg, .jpeg, .png, .gif, .pdf, .txt">
        <br>
        <input type="submit" value="Upload">
    </form>
</body>
</html>
```

From the logic of the `check()` function, our objective is to craft a PNG file that fulfils the specification to obtain the flag.

## Solution

This can be done quickly via Python's `PIL` and `exiftool`:

```python
from PIL import Image
 
im = Image.new(mode="RGBA", size=(690, 420))
im.putpixel((412, 309), (52, 146, 235, 123))
im.putpixel((12, 209), (42, 16, 125, 231))
im.putpixel((264, 143), (122, 136, 25, 213))

# This method will show image in any image viewer
im.save('web_perfect_picture_image.png')
```

```sh
# Mmodifying PNG data
exiftool -description='jctf{not_the_flag}' -title='kool_pic' -author='anon' web_perfect_picture_image.png
```

Upload `web_perfect_picture_image.png` via the UI to obtain flag.

## Flag

ictf{7ruly_th3_n3x7_p1c4ss0_753433}