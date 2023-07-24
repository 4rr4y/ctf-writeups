# Web - Idoriot (Imaginary CTF 2023)

## Problem

Obtain flag from web platform.

## Solution

Upon registering as any user, we obtain the following:

![Source code](images/web_idoriot1.png)

Observe that for the flag to display, we need `user_id=0`, which is the user ID of the admin user. When registering, we observe the following:

![register.php POST request](images/web_idoriot2.png)

Since `user_id` can be specified as POST data, we specify `user_id=0` for a new user registration to obtain the flag:

![register.php POST request](images/web_idoriot3.png)

## Flag

ictf{1ns3cure_direct_object_reference_from_hidden_post_param_i_guess}
