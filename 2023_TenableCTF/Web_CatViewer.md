# Web - Cat Viewer (Tenable CTF 2023)

## Problem

We are given a platform for viewing cats, for example:

![Cat Viewer default page](./images/web_catviewer1.png)

## Solution

Notice that `cat=Shelton` is in the GET request parameters. Changing it to `"` gives an error, indicating potential SQL injection:

![Cat Viewer Error](./images/web_catviewer2.png)

There are restrictions if we were to select too many cats (in terms of response size). Hence, the following union-based SQL injection requires something like `AND 1=0` for the query for cats to work well:

![First SQL Injection](./images/web_catviewer3.png)

We are aware that the 3rd field is printed. We also note the schema for the cats table in SQLite 3:

![Schema for cats](./images/web_catviewer4.png)

Hence, we can use the following payload to finally print the challenge flag:

```
" AND 1=0 UNION SELECT "1","2",flag,"4" FROM cats WHERE flag LIKE "flag{
```

![Challenge flag](./images/web_catviewer5.png)

## Flag

flag{a_sea_of_cats}