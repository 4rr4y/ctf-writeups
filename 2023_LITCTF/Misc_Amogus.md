# Misc - Kevin (LITCTF 2023)

## Problem

We are given the site, to which a suspicious `testing.jpg` exists:

![testing.jpg](./images/misc_amogus1.png)

## Solution

Running `exiftool` on the image gave us the flag in the `Make` field:

```sh
└─$ exiftool testing.jpg                                     
ExifTool Version Number         : 12.63
File Name                       : testing.jpg
Directory                       : .
File Size                       : 176 kB
File Modification Date/Time     : 2023:08:10 12:46:51+08:00
File Access Date/Time           : 2023:08:10 12:46:51+08:00
File Inode Change Date/Time     : 2023:08:10 12:46:51+08:00
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
X Resolution                    : 1
Y Resolution                    : 1
Exif Byte Order                 : Big-endian (Motorola, MM)
Make                            : s0m3t1m3s_th1ngs_4re_n0t_4lw4ys_wh4t_th3y_s33m
Resolution Unit                 : None
Y Cb Cr Positioning             : Centered
Image Width                     : 2560
Image Height                    : 1440
Encoding Process                : Progressive DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:4:4 (1 1)
Image Size                      : 2560x1440
Megapixels                      : 3.7
```

## Flag

LITCTF{s0m3t1m3s_th1ngs_4re_n0t_4lw4ys_wh4t_th3y_s33m}
