# Misc - kevin (LITCTF 2023)

## Problem

We are told this is a steganography problem. We find the following image of Kevin(?) on the website link given:

![Image of Kevin](./images/misc_kevin1.png)

## Solution

Since it is steganography on JPEG with `what's this LSB thing?` as it a hint, we use stegsolve and find the flag by checking the LSB for the RGB channels:

![Flag in image](./images/misc_kevin2.png)

## Flag

LITCTF{3d_printing_is_cool}